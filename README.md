# VQGAN-CLIP

# VQGAN in brief:
**VQGAN** stands for **Vector Quantized Generative Adversarial Network**, while **CLIP** stands for **Contrastive Image-Language Pretraining**. Whenever we say VQGAN-CLIP1, we refer to the interaction between these two networks. They’re separate models that work in tandem. The way they work is that VQGAN generates the images, while CLIP judges how well an image matches our text prompt. This interaction guides our generator to produce more accurate images.
