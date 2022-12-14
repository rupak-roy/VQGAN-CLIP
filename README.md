# VQGAN-CLIP

# VQGAN in brief:
**VQGAN** stands for **Vector Quantized Generative Adversarial Network**, while **CLIP** stands for **Contrastive Image-Language Pretraining**. Whenever we say VQGAN-CLIP1, we refer to the interaction between these two networks. They’re separate models that work in tandem. The way they work is that VQGAN generates the images, while CLIP judges how well an image matches our text prompt. This interaction guides our generator to produce more accurate images.

**VQGAN** employs  two-stage structure by learning an intermediary representation before feeding it to a transformer. However, instead of downsampling the image, VQGAN uses a codebook to represent visual parts. The authors did not model the image from a pixel-level directly, but instead from the codewords of the learned codebook.

![vqgan](https://compvis.github.io/taming-transformers/paper/teaser.png)


VQGAN was able to solve Transformer’s scaling problem by using an intermediate representation known as a codebook. This codebook serves as the bridge for the two-stage approach found in most image transformer techniques. The VQGAN learns a codebook of context-rich visual parts, whose composition is then modeled with an autoregressive transformer.

The codebook is generated through a process called vector quantization (VQ), i.e., the “VQ” part of “VQGAN.” Vector quantization is a signal processing technique for encoding vectors. It represents all visual parts found in the convolutional step in a quantized form, making it less computationally expensive once passed to a transformer network.

One can think of vector quantization as a process of dividing vectors into groups that have approximately the same number of points closest to them. Each group is then represented by a centroid (codeword), usually obtained via k-means or any other clustering algorithm. In the end, one learns a dictionary of centroids (codebook) and their corresponding members.

# Brief about CLIP:
    
**CLIP( Contrastive Language–Image Pre-training )** a model trained to determine which caption from a set of captions best fits with a given image.

OpenAI's CLIP model aims to learn generic visual concept with natural language supervision. This is because sandard computer vision model only work well on specific task, and require significant effort to adapt to a new task, hence have weak generalization capabilities. CLIP bridges the gap via learning directly from raw text about images at a web scale level.
CLIP does not directly optimize for the performance of a benchmark task (e.g. CIFAR), so as to keep its "zero-shot" capabilities for generalization. More interestingly, CLIP shows that scaling a simple pre-training task - which is to learn "which text matches with which image", is sufficient to achieve competitive zero-shot performance on many image classification datasets. 

![clipa](https://openaiassets.blob.core.windows.net/$web/clip/draft/20210104b/overview-a.svg)

![clipb](https://openaiassets.blob.core.windows.net/$web/clip/draft/20210104b/overview-b.svg)

CLIP trains a text encoder (Bag-of-Words or Text Transformer) and an image encoder (ResNet or Image Transformer) which learns feature representations of a given pair of text and image. The scaled cosine similarity matrix of the image and text feature is computed, and the diagonal values are minimized to force the image feature match its corresponding text feature.

# VQGAN+CLIP:

CLIP guides VQGAN towards an image that is the best match to a given text. CLIP is the “Perceptor” and VQGAN is the “Generator”. VQGAN like all GANs VQGAN takes in a noise vector, and outputs a (realistic) image. CLIP on the other hand takes in an image and text, and outputs the image features and text features respectively. The similarity between image and text can be represented by the cosine similarity of the learnt feature vectors.

By leveraging CLIPs capacities as a “steering wheel”, we can use CLIP to guide a search through VQGAN’s latent space to find images that match a text prompt very well according to CLIP.

source - [VQGAN+CLIP — How does it work?](https://alexasteinbruck.medium.com/vqgan-clip-how-does-it-work-210a5dca5e52)

![VQGAN+CLIP — How does it work?](https://ljvmiranda921.github.io/assets/png/vqgan/clip_vqgan_with_image.png)

Image source - [The Illustrated VQGAN](https://ljvmiranda921.github.io/assets/png/vqgan/clip_vqgan_with_image.png)

# Try out with different combinations
![info](https://raw.githubusercontent.com/rupak-roy/VQGAN-CLIP/main/1__vwNbasrHuw5ScVIugi4aw.jpeg)

![info](https://raw.githubusercontent.com/rupak-roy/VQGAN-CLIP/main/1_yVHBKcdoGDs7SNZ21r94Bw.jpg)

# References

* [VQGAN_CLIP( hHugging Face )](https://huggingface.co/spaces/akhaliq/VQGAN_CLIP)
* [The Illustrated VQGAN](https://ljvmiranda921.github.io/notebook/2021/08/08/clip-vqgan/)
* [VQGAN+CLIP — How does it work?](https://alexasteinbruck.medium.com/vqgan-clip-how-does-it-work-210a5dca5e52)
* [Image Generation Based on Abstract Concepts Using CLIP + BigGAN](https://wandb.ai/gudgud96/big-sleep-test/reports/Image-Generation-Based-on-Abstract-Concepts-Using-CLIP-BigGAN--Vmlldzo1MjA2MTE)
