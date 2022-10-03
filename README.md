# VQGAN-CLIP

# VQGAN in brief:
**VQGAN** stands for **Vector Quantized Generative Adversarial Network**, while **CLIP** stands for **Contrastive Image-Language Pretraining**. Whenever we say VQGAN-CLIP1, we refer to the interaction between these two networks. They’re separate models that work in tandem. The way they work is that VQGAN generates the images, while CLIP judges how well an image matches our text prompt. This interaction guides our generator to produce more accurate images.

**VQGAN** employs  two-stage structure by learning an intermediary representation before feeding it to a transformer. However, instead of downsampling the image, VQGAN uses a codebook to represent visual parts. The authors did not model the image from a pixel-level directly, but instead from the codewords of the learned codebook.

![vqgan](https://compvis.github.io/taming-transformers/paper/teaser.png)


VQGAN was able to solve Transformer’s scaling problem by using an intermediate representation known as a codebook. This codebook serves as the bridge for the two-stage approach found in most image transformer techniques. The VQGAN learns a codebook of context-rich visual parts, whose composition is then modeled with an autoregressive transformer.

The codebook is generated through a process called vector quantization (VQ), i.e., the “VQ” part of “VQGAN.” Vector quantization is a signal processing technique for encoding vectors. It represents all visual parts found in the convolutional step in a quantized form, making it less computationally expensive once passed to a transformer network.

One can think of vector quantization as a process of dividing vectors into groups that have approximately the same number of points closest to them. Each group is then represented by a centroid (codeword), usually obtained via k-means or any other clustering algorithm. In the end, one learns a dictionary of centroids (codebook) and their corresponding members.
___
