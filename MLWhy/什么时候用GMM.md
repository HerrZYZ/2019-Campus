Gaussian mixture model可以用来聚类，但我们什么时候用它而不是用像KMeans之类的方法呢？

GMM假设数据是来自几个不同的高斯分布，并且这些高斯分布的均值和方差都是从数据中学到。对比K-Means, 一般的，我们可以认为K-Means是特殊的GMM, 
其假设数据具有固定的方差，协方差为0，并且训练时是使用Hard EM。所以K-Means期望cluster内的数据是球形分布的，而一般的GMM则可以处理椭圆形的cluster。

![GMM](http://scikit-learn.org/0.15/_images/plot_gmm_classifier_0011.png)
