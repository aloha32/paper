# paper
自用paper总结
# 2024.10.23
上传了paper文件包含8篇文章，两个坑待填，KAN和Hiera
# 2024.10.24
[Hiera](https://github.com/facebookresearch/hiera)论文看了好久，最终卡在图4，发现Hiera与MAE的关系机器紧密，[MAE](https://openaccess.thecvf.com/content/CVPR2022/html/He_Masked_Autoencoders_Are_Scalable_Vision_Learners_CVPR_2022_paper)是何凯明CVPR2022的作品(稍微看了一眼，好像没给代码，难道只是一种训练方法？)，明天先读一下MAE补充一下背景知识吧，ViT也有点忘了，明天小看一下。
# 2024.10.26
[MAE论文图1-**架构**](https://github.com/aloha32/paper/blob/main/MAE-P1.jpg)初次看根本看不懂，什么mask，什么token，什么decoder，根本搞不懂。问了GPT恍然大悟。
```
图1展示了**MAE（Masked Autoencoder）架构**的流程，主要分为三个部分：输入、编码器-解码器、输出目标。下面详细解释图中各部分的流程：

1. **输入（input）**：
   - 输入图像被划分成不重叠的小块（patches），例如16x16像素的图像块。
   - 在预训练阶段，这些图像块中的大部分（通常为75%）被随机掩盖（图中用灰色方块表示）。这样，仅有少部分的图像块是可见的（图中为彩色部分）。

2. **编码器（encoder）**：
   - 编码器只作用于**可见的图像块**，即没有被掩码的部分。与传统自编码器不同，MAE的编码器并不接收掩码标记作为输入，而是直接对可见图像块进行编码。
   - 编码器的任务是从可见的部分学习出图像的潜在表示（latent representation），这些表示用一系列蓝色方块表示。

3. **解码器（decoder）**：
   - 在编码完成之后，**掩码标记（mask tokens）**被引入，并与编码后的可见图像块组合在一起。每个掩码标记用灰色方块表示，代表被掩盖的图像块。
   - 解码器处理这组完整的编码块（包括编码后的可见块和掩码标记），并通过生成缺失图像块来**重建完整的图像**。解码器的计算量较小，通常是轻量级的。
   - 解码器的输出为一组重建的图像块（红色方块），这些块代表了模型对被掩盖区域的预测。

4. **目标（target）**：
   - 最终，解码器重建的图像与原始输入图像的像素级别进行对比（只对被掩盖的区域进行损失计算）。模型通过最小化重建误差来优化自我监督学习任务。
   - 在预训练结束后，解码器被丢弃，编码器则用于**下游任务**（如图像分类或目标检测），此时输入为完整的、没有掩盖的图像。

**总结**：
图1展示了MAE如何通过随机掩盖大部分图像块，并训练编码器-解码器架构来重建图像。这种方法有助于模型学习全局特征，并能够在图像自监督学习中实现良好的性能。
```
