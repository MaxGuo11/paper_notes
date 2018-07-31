https://arxiv.org/abs/1803.07133

1. Traditional: MLE最大似然估计

   Recently:  reinforcement learning, 

​		re-parameterization tricks（MLE的特例）

​		generative adversarial nets

2. 几种结构：

   普通NN：不能long-term

   RNN，GRU，LSTM：exposure bias的问题

   supervised learning, RL && GAN: 解决部分问题同时又有一些新的问题

   * sl with MLE：现有大部分使用的方法，易于收敛，算法稳定等特点；存在exposure bias问题，training stage与inference stage不同源，在inference时需要提供一个prefix，model产生于training data，而我们想要的是基于inference的语境，从而造成结果的偏差；而且，text越长这种平衡越明显，因此难以用于long text generation tasks
   * Schedule sampling(ss)提出，意在减小training stage和inference stage的差别，但是会造成不稳定的结果
   * PG-BLEU：使用reinforce的方法优化BLEU，有两个问题：1. BLEU计算量大 2. BLEU只计算generated text 和corpus的n-gram similarity，所以会造成不稳定现象
   * GAN：可以减少exposure bias，eg. SegGAN。仍有两个问题：1. gradient vanishing，对抗网络不平衡是，discriminator全面压倒generator导致其得不到更新 2. 产生结果过于单一
   * MaliGAN：用rescaled scores更新reward signal（discriminator产生的score），可以解决：1. gradient vanishing的问题；2.产生结果单一的问题
   * RankGAN：用ranking score代替binary classification，可以积极convergence的问题，但是需要从corpus中sample，所以计算量很大
   * Bootstrapped Ranking Activation（BRA）来自于seqGAN，在每一个batch使用ranking information recale reward，
   * LeakGAN，解决长文本问题，40个word。

​			