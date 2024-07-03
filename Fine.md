# IPAdapter
## Abstract & Introduction
text-to-image models:  GLIDE,DALL-E,Imagen,Stable-Diffusion

以往image prompt Finetuning的问题:

* eliminates the original ability to generate images using text
* 不可复用 not reusable

重点提到了ControlNet与T2I-Adapter，作者认为它们使用的方法大都是将CLIP里image encoder的feature映射到一个新的image feature，再和text feature一起送入Unet去学习

但是最后呈现的结果是"partially faithful to the prompt image"，也就是不忠于原图的

![image-20240702144352324](E:\笔记\image-20240702144352324.png)

所以作者就想，问题可能出现在cross attention layer这里，attention中的key 和 value是用来训练text feature的，这也就会导致一部分image feature的缺失，因此本文提出了一种<mark>decoupled cross-attention</mark>来单独设计给image feature，以解决这个问题

## Method

![image-20240702133340610](E:\笔记\image-20240702133340610.png)



![image-20240702140936434](E:\笔记\image-20240702140936434.png)

其实就是text feature是冻结的cross attention layer，而image的是可以训练的，然后再把它们的权重加起来就行

# T2I-Adapter

<<T2I-Adapter: Learning Adapters to Dig out More Controllable Ability for Text-to-Image Diffusion Models>>AAAI 2024

## 
