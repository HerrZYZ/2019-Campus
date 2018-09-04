### UserCF和ItemCF的比较
>UserCF的推荐结果着重于反映和用户兴趣相似的小群体的热点，而ItemCF的推荐结果着重于维系用户的历史兴趣。换句话说，UserCF的推荐更社会化，反映了用户所在的
小型兴趣群体中物品的热门程度，而ItemCF的推荐更加个性化，反映了用户自己的兴趣传承。

新闻网站使用UserCF, 电子商务，电影网站使用ItemCF, why?

新闻网站的特点之一是new item不断出现，对于new item，使用UserCF时, 只要有一个user对该item产生行为，则可以将其推荐给相似user。若使用ItemCF, 
不更新item的相似矩阵表就无法推荐new item。并且对于new user, 可以简单地推荐热点新闻。

电子商务网站的特点之一是用户数目多，个性化粒度比较细。使用ItemCF可以帮助用户发现和他研究领域相关的物品。
