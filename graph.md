# Deep Learning on Graphs

[General](README.md) | Graphs

## Introduction

* [How do I generalize convolution of neural networks to graphs?](https://www.quora.com/How-do-I-generalize-convolution-of-neural-networks-to-graphs) [Spatial vs. Spectral]
* [Deep Learning on Graphs](https://figshare.com/articles/Deep_Learning_on_Graphs/4491686) [Slides]
* [Gated Graph Sequence Neural Networks](https://arxiv.org/pdf/1511.05493.pdf)
* [SchNet: A continuous-filter convolutional neural network for modeling quantum interactions](https://arxiv.org/pdf/1706.08566.pdf) (NIPS 2017)

## Geometric Deep Learning

* [Geometric deep learning](http://geometricdeeplearning.com/) [Collection of links]
* [Geometric deep learning: going beyond Euclidean data](https://arxiv.org/pdf/1611.08097.pdf)
* [Geometric deep learning on graphs and manifolds using mixture model CNNs](https://arxiv.org/pdf/1611.08402.pdf)
* [Geodesic convolutional neural networks on Riemannian manifolds](https://arxiv.org/pdf/1501.06297.pdf)
* [Geometric deep learning on graphs](https://www.dropbox.com/s/4l6m32tg9yecvow/CVPR%20GDL.pdf?dl=0) [Slides (228MB)]
* [Robust Spatial Filtering with Graph Convolutional Neural Networks](https://arxiv.org/pdf/1703.00792.pdf) (Graph-CNNS + Graph Embed Pooling) [[Code](https://github.com/fps7806/Graph-CNN)]

## Spectral Approach

* [Spectral Graph Theory](http://www.math.ucsd.edu/~fan/research/revised.html)
* [Wavelets on Graphs via Spectral Graph Theory](https://arxiv.org/pdf/0912.3848.pdf)
* [The Emerging Field of Signal Processing on Graphs](https://arxiv.org/pdf/1211.0053.pdf)
* [Discrete Laplace-Beltrami Operators for Shape Analysis and Segmentation](https://reuter.mit.edu/papers/reuter-smi09.pdf)
* [What's the intuition behind a Laplacian matrix](https://www.quora.com/Graph-Theory-Whats-the-intuition-behind-a-Laplacian-matrix)

### Architectures

* [Convolutional Neural Networks on Graphs with Fast Localized Spectral Filtering](https://arxiv.org/pdf/1606.09375.pdf) [[TF Code](https://github.com/mdeff/cnn_graph)] [[PyTorch Code](https://github.com/xbresson/graph_convnets_pytorch)] [[Notebook](http://nbviewer.jupyter.org/github/mdeff/cnn_graph/blob/outputs/usage.ipynb)]
* [Semi-Supervised Classification with Graph Convolutional Networks](https://arxiv.org/pdf/1609.02907v3.pdf) [[Code](https://github.com/tkipf/gcn)] [[Explanation](http://tkipf.github.io/graph-convolutional-networks/)] [[Criticism](http://www.inference.vc/how-powerful-are-graph-convolutions-review-of-kipf-welling-2016-2/)] [[Review](https://openreview.net/forum?id=SJU4ayYgl)]
* [CayleyNets: Graph Convolutional Neural Networks with Complex Rational Spectral Filters](https://arxiv.org/pdf/1705.07664.pdf)
* [Spectral Networks and Deep Locally Connected Networks on Graphs](https://arxiv.org/pdf/1312.6203.pdf)
* [Convolutional Neural Networks auf Graphrepräsentationen von Bildern](https://github.com/rusty1s/deep-learning-on-graphs/tree/master/masterthesis) [[Code](https://www.github.com/rusty1s/embedded_gcnn)]
* [Deep Convolutional Networks on Graph-Structured Data](https://arxiv.org/pdf/1506.05163.pdf)
* [Convolutional Networks on Graphs for Learning Molecular Fingerprints](https://hips.seas.harvard.edu/files/duvenaud-graphs-nips-2015.pdf) [Node-degree specific weight matrices]
* [Graph image representation from convolutional neural networks](https://www.google.ch/patents/US9418458)
* [Dynamic Graph Convolutional Networks](https://arxiv.org/pdf/1704.06199.pdf)

#### Autoencoder

* [Automatic chemical design using a data-driven continuous representation of molecules](https://arxiv.org/pdf/1610.02415.pdf)
* [Variational Graph Auto-Encoders](https://arxiv.org/abs/1611.07308)
* [GraphVAE: Towards Generation of Small Graphs Using Variational Autoencoders](https://openreview.net/forum?id=SJlhPMWAW)
* [Learnign Deep Generative Models of Graphs](https://openreview.net/forum?id=Hy1d-ebAb)
* [Learning Graphical State Transitions](http://www.hexahedria.com/files/2017learninggraphical.pdf)
* [GRASS: Generative Recursive Autoencoders for Shape Structure](https://arxiv.org/abs/1705.02090) [[Reddit](https://www.reddit.com/r/MachineLearning/comments/7j70n8/r_grass_generative_recursive_autoencoders_for/)]

### Propagation rules

* **SGCNN (Spectral Graph Convolutional Neural Network):**
  * $\tilde{L} := L - I$
  * $\overline{F}_0 := F\_{in} W_0$
  * $\overline{F}_1 := \tilde{L} F\_{in} W_1$
  * $\overline{F}_k := \left(2\tilde{L} \overline{F}\_{k-1} - \overline{F}\_{k-2} \right) W_k$
  * $W \in \mathbb{R}^{(K+1) \times M\_{in} \times M\_{out}}$

$$
F_{out} := \sum\_{k=0}^K \overline{F}\_k
$$

* **GCN (Graph Convolutional Network):**
  * $\tilde{A} := A + I$
  * $\tilde{D} := D + I$
  * $W \in \mathbb{R}^{M\_{in} \times M\_{out}}$

$$
F_{out} := \tilde{D}^{-\frac{1}{2}} \tilde{A} \tilde{D}^{-\frac{1}{2}} F\_{in} W
$$

* **EGCNN (Embedded Graph Convolutional Neural Network):**
  * Number of partitions $P$
  * closed B-Spline function $\mathrm{N}^K\_p$ with degree $K$ and node vector $\tau := [\alpha_0, \ldots, \alpha_{P+K}]^{\top}$ with $\alpha_p := 2\pi p / P$
  * $W \in \mathbb{R}^{(P+1) \times M\_{in} \times M\_{out}}$

$$
F_{out} := \tilde{D}^{-1}\_{dist} F\_{in} W\_{P+1} + \sum\_{p=0}^{P-1} \left( \mathrm{N}^K_p(A\_{rad}) \odot \left( \tilde{D}\_{dist}^{-\frac{1}{2}} \tilde{A}\_{dist} \tilde{D}^{-\frac{1}{2}}\_{dist} \right) \right) F\_{in} W\_{p+1}
$$

## Spatial Approach

* [Learning Convolutional Neural Networks for Graphs](https://arxiv.org/pdf/1605.05273.pdf) [[Slides](http://www.matlog.net/icml2016_slides.pdf)]
* [Generalizing CNNs for data structured on locations irregularly spaced out](https://arxiv.org/pdf/1606.01166.pdf)

## Isomorphism

* [The Weisfeiler-Lehman Method and Graph Isomorphism Testing](https://arxiv.org/pdf/1101.5211v1.pdf)
* [Pratical graph isomorphism, II](https://arxiv.org/pdf/1301.1493v1.pdf)
* [Canonical Labelings with Nauty](https://computationalcombinatorics.wordpress.com/2012/09/20/canonical-labelings-with-nauty/) [[Code](http://pallini.di.uniroma1.it)] [[Python Wrapper](https://web.cs.dal.ca/~peter/software/pynauty/html/index.html)]

## Graph Kernels

* [Graph Kernels](https://edoc.ub.uni-muenchen.de/7169/1/Borgwardt_KarstenMichael.pdf)
* [Image Classification with Segmenation Graph Kernels](http://www.di.ens.fr/~fbach/harchaoui_bach_cvpr07.pdf)
* [Deep Graph Kernels](http://dl.acm.org/citation.cfm?id=2783417)

## Coarsening

* [Weighted Graph Cuts without Eigenvectors: A Multivel Approach](http://www.cs.utexas.edu/users/inderjit/public_papers/multilevel_pami.pdf)
