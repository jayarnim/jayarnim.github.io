---
order: 1
title: Deep Learning based Collaborative Filtering
date: 2024-02-15
categories: [RECOMMENDER SYSTEM, 2.mlp based collaborative filtering]
tags: [AI Application, Recommender System, Collaborative Filtering]
math: true
description: >-
    Zhang, S., Yao, L., Sun, A., & Tay, Y.</br>
    (2019).</br>
    <a href="https://doi.org/10.1145/3285029">Deep learning based recommender system: A survey and new perspectives.</a></br>
    ACM computing surveys (CSUR), 52(1), 1-38.
image:
    path: /_post_refer_img/RecommenderSystem/2.MLP/Thumbnail.jpg
---

## MLP
-----

- **Merit**
    - User, Item Representation Learning
    - Matching function learning
    - Modeling nonlinear interactions between users and items

### ID Embedding

- **ID Embedding**: Embedding user and item identifiers into a low-dimensional vector space

    ![01](/_post_refer_img/RecommenderSystem/2.MLP/01-01.png){: width="100%"}

- [`NCF`](https://doi.org/10.1145/3038912.3052569): ID Embedding based Latent Factor Model\\
(Linear and Non-Linear Matching Function Ensemble)
    - He, X., Liao, L., Zhang, H., Nie, L., Hu, X., & Chua, T. S.\\
    (2017, April).\\
    Neural collaborative filtering.\\
    In Proceedings of the 26th international conference on world wide web (pp. 173-182).

### History Embedding

- **History Embedding**: Generate each user and item expressions based on past interaction history

    ![02](/_post_refer_img/RecommenderSystem/2.MLP/01-02.png){: width="100%"}

    - by aggregating the raw representations of one entity with which the another entity interacted
    - by reducing the dimensionality of the user-item interaction matrix and its transpose

- [`DMF`](https://doi.org/10.24963/ijcai.2017/447): History Embedding based Latent Factor Model\\
(Representation Learning)
    - Xue, H. J., Dai, X., Zhang, J., Huang, S., & Chen, J.\\
    (2017, August).\\
    Deep matrix factorization models for recommender systems.\\
    In IJCAI (Vol. 17, pp. 3203-3209).

- [`DeepCF`](https://doi.org/10.48550/arXiv.1901.04704): History Embedding based Latent Factor Model\\
(Representation Learning and Matching Function Learning Ensemble)
    - Deng, Z. H., Huang, L., Wang, C. D., Lai, J. H., & Yu, P. S.\\
    (2019, July).\\
    Deepcf: A unified framework of representation learning and matching function learning in recommender system.\\
    In Proceedings of the AAAI conference on artificial intelligence (Vol. 33, No. 01, pp. 61-68).

- [`J-NCF`](https://doi.org/10.1145/3343117): History Embedding based Latent Factor Model\\
(Representation Learning and Matching Function Learning Serial)
    - Chen, W., Cai, F., Chen, H., & Rijke, M. D.\\
    (2019).\\
    Joint neural collaborative filtering for recommender systems.\\
    ACM Transactions on Information Systems (TOIS), 37(4), 1-30.

### Dual Embedding

- **Dual Embedding**: Use both ID Embedding and History Embedding

    ![03](/_post_refer_img/RecommenderSystem/2.MLP/01-03.png){: width="100%"}

- [`DNCF`](https://doi.org/10.48550/arXiv.2102.02549): Dual Embedding based Latent Factor Model\\
(Ensemble combining ID embedding and history embedding)
    - He, G., Zhao, D., & Ding, L.\\
    (2021).\\
    Dual-embedding based neural collaborative filtering for recommender systems.\\
    arXiv preprint arXiv:2102.02549.

### Distance Embedding

- **Distance Embedding**: Calculate Similarity through distance, not inner product, outer product, or concatenation

- [`DDFL`](https://doi.org/10.1007/978-3-030-59419-0_36): Distance Embedding based Latent Factor Model
    - Shah, S. T. U., Li, J., Guo, Z., Li, G., & Zhou, Q.\\
    (2020, September).\\
    DDFL: a deep dual function learning-based model for recommender systems.\\
    In International Conference on Database Systems for Advanced Applications (pp. 590-606).\\
    Cham: Springer International Publishing.

## AutoEncoder
-----

![04](/_post_refer_img/RecommenderSystem/2.MLP/01-04.png){: width="100%"}

- **Merit**
    - Restore the user-item interaction matrix
    - Dimensionality Reduction of the user-item interaction matrix
    - Feature Extraction

- [`AutoRec`](https://doi.org/10.1145/2740908.2742726): AutoEncoder Application
    - Sedhain, S., Menon, A. K., Sanner, S., & Xie, L.\\
    (2015, May).\\
    Autorec: Autoencoders meet collaborative filtering.\\
    In Proceedings of the 24th international conference on World Wide Web (pp. 111-112).

- [`CDAE`](https://doi.org/10.1145/2835776.2835837): Denoising AutoEncoder Application
    - Wu, Y., DuBois, C., Zheng, A. X., & Ester, M.\\
    (2016, February).\\
    Collaborative denoising auto-encoders for top-n recommender systems.\\
    In Proceedings of the ninth ACM international conference on web search and data mining (pp. 153-162).

- [`VACF`](https://doi.org/10.1145/3178876.3186150): Variational AutoEncoder Application
    - Liang, D., Krishnan, R. G., Hoffman, M. D., & Jebara, T.\\
    (2018, April).\\
    Variational autoencoders for collaborative filtering.\\
    In Proceedings of the 2018 world wide web conference (pp. 689-698).

## CNN
-----

- **Merit**
    - Modeling interdimensional high-level interactions between users and items

- [`ConvNCF`](https://doi.org/10.48550/arXiv.1808.03912): Using CNN as Matching Function
    - He, X., Du, X., Wang, X., Tian, F., Tang, J., & Chua, T. S.\\
    (2018).\\
    Outer product-based neural collaborative filtering.\\
    arXiv preprint arXiv:1808.03912.

- [`COMET`](https://doi.org/10.1145/3588576): Using CNN as Aggregating Histories
    - Lin, Z., Feng, L., Guo, X., Zhang, Y., Yin, R., Kwoh, C. K., & Xu, C.\\
    (2023).\\
    Comet: Convolutional dimension interaction for collaborative filtering.\\
    ACM Transactions on Intelligent Systems and Technology, 14(4), 1-18.

## Attention Mechanism
-----

- **Merit**
    - Select important information and remove noise
    - Aggregate histories

- [`DACR`](https://doi.org/10.3390/app122010594): History Embedding based Latent Factor Model Assist.
    - Cui, C., Qin, J., & Ren, Q.\\
    (2022).\\
    Deep collaborative recommendation algorithm based on attention mechanism.\\
    Applied Sciences, 12(20), 10594.

- [`DRNet`](https://doi.org/10.1109/ACCESS.2020.3002102): Aggregate user's histories
    - Ji, D., Xiang, Z., & Li, Y.\\
    (2020).\\
    Dual relations network for collaborative filtering.\\
    IEEE Access, 8, 109747-109757.

- [`DELF`](https://doi.org/10.24963/ijcai.2018/462): Aggregate user and item's histories
    - Cheng, W., Shen, Y., Zhu, Y., & Huang, L.\\
    (2018, July).\\
    DELF: A dual-embedding based deep latent factor model for recommendation.\\
    In IJCAI (Vol. 18, pp. 3329-3335).