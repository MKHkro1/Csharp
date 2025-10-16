为什么蓝飘飘要给僵尸写takedamage和getdamage两个功能差不多的方法 

可能…… 一个是造成固定伤害，一个是反伤？

不一样的
getdamage是计算减伤之类的 
takedamage是根据getdamage返回的伤害值，再根据对应的伤害类型，来结算伤害

但是，两个诅咒僵尸都只改了getdamage方法
然后在getdamage里面判断是否转移伤害 

简单来说……take只负责结算伤害？