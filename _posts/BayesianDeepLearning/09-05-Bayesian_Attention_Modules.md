---
order: 2
title: Bayesian Attention Modules
date: 2024-09-05
categories: [Research Interest, Bayesian Deep Learning]
tags: [Deep Learning, Bayesian, Information Theory, Variational Inference]
math: true
description: >-
    <ul type="square">
    <li><strong>Title</strong>: <a href="https://arxiv.org/abs/2010.10604"><code>Bayesian Attention Modules</code></a></li>
    <li><strong>Publisher</strong>: <em>NeurlPS</em></li>
    <li><strong>Published</strong>: <em>2020</em></li>
    </ul>
image:
    path: /_post_refer_img/BayesianDeepLearning/Thumbnail.jpg
---

$$\begin{aligned}
\mathbf{P} &= \text{Bayesian-Attention}\left(\mathbf{U}, \mathbf{V}, \mathbf{V}\right)\\
\mathbf{Q} &= \text{Bayesian-Attention}\left(\mathbf{V}, \mathbf{U}, \mathbf{U}\right)\\
\mathbf{X} &= \mathbf{P} \cdot \mathbf{Q}\\
\mathbf{Z} &= \text{VAE-Encoder}\left(\mathbf{X}\right)\\
\hat{\mathbf{X}} &= \text{VAE-Decoder}\left(\mathbf{Z}\right)
\end{aligned}$$



(1) 사전 확률 분포 결정

$$\begin{aligned}
p\left(W ; \eta\right)
&= \sigma_{\text{Softmax}}\left[\mathcal{F}^{(2)}\left(\sigma_{\text{ReLU}}\left[\mathcal{F}^{(1)}\left(K\right)\right]\right)\right]
\end{aligned}$$