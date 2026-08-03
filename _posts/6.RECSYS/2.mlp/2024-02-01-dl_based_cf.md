---
order: 1
title: Deep Learning based Collaborative Filtering
date: 2024-02-01
categories: [6.RECOMMENDER SYSTEM, 2.mlp based collaborative filtering]
tags: [ai application, recommender system, collaborative filtering, latent factor model, mlp]
math: true
description: >-
    Zhang, S., Yao, L., Sun, A., & Tay, Y.</br>
    (2019).</br>
    <a href="https://doi.org/10.1145/3285029">Deep learning based recommender system: A survey and new perspectives.</a></br>
    ACM computing surveys (CSUR), 52(1), 1-38.
image:
    path: /assets/img/posts/6.RECSYS/2.mlp/Thumbnail.jpg
---

## summary

- mlp (latent factor model):
    - entry-wise learning
    - representation learning
    - matching function learning
    - modeling nonlinear interactions

- cnn:
    - modeling cross-dimensional interactions
    - aggregate histories

- attention mechanism:
    - select important information and remove noise
    - aggregate histories

## mlp

- bilinear interaction vs. nonlinear interaction:
    - `NeuMF` He, X., Liao, L., Zhang, H., Nie, L., Hu, X., & Chua, T. S. (2017, April). Neural collaborative filtering. In Proceedings of the 26th international conference on world wide web (pp. 173-182).

- one-hot matrix vs. user-item interaction matrix (init. information to generate embedding):
    - `DMF` Xue, H. J., Dai, X., Zhang, J., Huang, S., & Chen, J. (2017, August). Deep matrix factorization models for recommender systems. In IJCAI (Vol. 17, pp. 3203-3209).
    - `DNMF` He, G., Zhao, D., & Ding, L. (2021). Dual-embedding based neural collaborative filtering for recommender systems. arXiv preprint arXiv:2102.02549.

- representation learning vs. matching function learning:
    - `CFNet` Deng, Z. H., Huang, L., Wang, C. D., Lai, J. H., & Yu, P. S. (2019, July). Deepcf: A unified framework of representation learning and matching function learning in recommender system. In Proceedings of the AAAI conference on artificial intelligence (Vol. 33, No. 01, pp. 61-68).
    - `J-NCF` Chen, W., Cai, F., Chen, H., & Rijke, M. D. (2019). Joint neural collaborative filtering for recommender systems. ACM Transactions on Information Systems (TOIS), 37(4), 1-30.

- can the distance between vectors in the latent space be considered to reflect preferences?
    - `DDFL` Shah, S. T. U., Li, J., Guo, Z., Li, G., & Zhou, Q. (2020, September). DDFL: a deep dual function learning-based model for recommender systems. In International Conference on Database Systems for Advanced Applications (pp. 590-606). Cham: Springer International Publishing.

## cnn

- inner product vs. outer product:
    - `ConvNCF` He, X., Du, X., Wang, X., Tian, F., Tang, J., & Chua, T. S. (2018). Outer product-based neural collaborative filtering. arXiv preprint arXiv:1808.03912.

- history aggregation:
    - `COMET` Lin, Z., Feng, L., Guo, X., Zhang, Y., Yin, R., Kwoh, C. K., & Xu, C. (2023). Comet: Convolutional dimension interaction for collaborative filtering. ACM Transactions on Intelligent Systems and Technology, 14(4), 1-18.

## attention mechanism

- denoiser:
    - `DACR` Cui, C., Qin, J., & Ren, Q. (2022). Deep collaborative recommendation algorithm based on attention mechanism. Applied Sciences, 12(20), 10594.

- latent factor model vs. item based collaborative filtering:
    - `DRNet` Ji, D., Xiang, Z., & Li, Y. (2020). Dual relations network for collaborative filtering. IEEE Access, 8, 109747-109757.

- history aggregation:
    - `DELF` Cheng, W., Shen, Y., Zhu, Y., & Huang, L. (2018, July). DELF: A dual-embedding based deep latent factor model for recommendation. In IJCAI (Vol. 18, pp. 3329-3335).