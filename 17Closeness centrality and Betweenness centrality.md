#                            接近度中心性和阶数中心性

### 一、接近度中心性

##### 1、定义

接近度中心性(closeness centrality, CC<sub>i</sub>)是对各个节点到节点的终点之间最短路径平均长度的考量，指最短的路径总和的倒数和其他节点数量的乘积，简称**接近数**。

##### 2、相关参数

①用d<sub>ij</sub>表示节点i到节点j的最短路径长度。

②对于网络中的每一个节点i，可以用d<sub>i</sub>表示，既有
$$
d_i=\frac{1}{N}\cdot\sum_{j=1}^{N}{d_{ij}}\tag{1}
$$
所以，d<sub>i</sub>值的相对大小也在某种程度上反映了节点i在网络中的相对重要性，且d<sub>i</sub>的值越小意味着节点更接近其他节点。

##### 3、公式

$$
CC_i=\frac{N}{\sum_{j=1}^{N}{d_{ij}}}=\frac{1}{d_i}\tag{2}
$$

<!--注：综合（1)(2)式可将d<sub>i</sub>的倒数定义为节点i的接近度中心性。-->

##### 4、重要性质意义

①接近数最大的节点对于信息流动具有最佳的观察视野。

②接近度中心性表示节点与其他节点交换信息的频率，该方法考虑了目标节点到其他节点的所有最短路径，从而可以消除异常长路径的干扰。

③接近度中心性接近度中心性评价的是一个点到其他点的距离的总和，这个总和越小则该点到其他点的路径越短，说明这个点处于核心位置。

##### 5、举例

![image-20211017202542877](C:\Users\lj\AppData\Roaming\Typora\typora-user-images\image-20211017202542877.png)

如图中网络，以A点为例：

图中点的个数 N = 11：

与A相连的路径为1的共4个点，为B,D,E,F
与A相连的路径为2的共3个点，为G,C,H
与A相连的路径为3的共3个点，为I,J,K

可得A的平均距离为$d(A)=\frac{1}{11}(4+2*3=3*3)$，则A的接近度中心性$CC_i=\frac{1}{d(A)}$。

### 二、介数中心性

##### 1、定义

介数中心性(betweenness centrality, BC<sub>i</sub>)是指个节点担任其它两个节点之间最短路径的桥梁的次数除以所有的最短路径数量的比例。

##### 2、相关参数

①g<sub>st</sub>表示从节点s到节点t的最短路径数目。

②$n_{st}^i$表示为节点s到节点t的g$_{st}$条最短路径中经过节点i的最短路径的数目。

③用$\frac{(N-1)(N-2)}{2}$表示网络中除去节点自身后的节点对个数m。

④用$N^2$表示网络中不去除节点自身的节点对个数m。

##### 3、公式

$$
BC_i=\sum_{s\neq i\neq t}\frac{n_{st}^i}{g_{st}}\tag{3}
$$

则对于一个包含N个节点的联通网络，基于两种不同情况下的节点对个数，有两种不同的归一化介数定义：

①在网络中去除节点自身后的节点个数的情况下（即$m=\frac{(N-1)(N-2)}{2}$时），归一化介数定义为：
$$
BC_i=\frac{(N-1)(N-2)}{2}\sum_{s\neq i\neq t}\frac{n_{st}^i}{g_{st}}\tag{4}
$$
②在网络中包括节点自身的节点对个数的情况下（即$m=N^2$时）,归一化介数定义为：
$$
BC_i=\frac{1}{N^2}\sum_{s\neq i\neq t}\frac{n_{st}^i}{g_{st}}\tag{5}
$$
尽管公式（4）（5）在计算时结果会有些不同，但不会影响网络中的节点按介数大小的排序结果，而后者通常才是我们关心的。

##### 4、重要性质意义

①**介数中心性刻画了节点i对于网络中节点对之间沿着最短路径传输信息的控制能力。**如果节点s和节点t之间没有路径（即$n_{st}^i=g_{st}=0$）,或者节点i没有位于节点s和节点t之间的任何一条最短的路径上（即$n_{st}=0$）,那么显然节点i对于节点s和节点t之间的传输信息没有直接的控制能力。（如果$n_{st}^i=g_{st}=0$,那么定义$\frac{n_{st}^i}{g_{st}}=0$）

②从控制信息传输的角度而言，**介数越高的节点其重要性也越大，去除这些节点后对网络传输的影响也越大**。尽管在实际网络中，节点对之间的传输频率并不都一样，而且也并非所有的传输都是基于最短路径的，介数仍然近似刻画了节点对网络上信息流动的影响力。

③介数中心性类似于一个节点在整体网络中担任最短路径桥梁的能力，体现了该节点流通性的能力。

④介数最高的节点对于网络中信息的流动具有最大的控制力。

##### 5、举例

##### ![image-20211017204141345](C:\Users\lj\AppData\Roaming\Typora\typora-user-images\image-20211017204141345.png)

以1节点为例，计算其介数中心性为：

从5->4，最短路径为（5，1，4），该路径经过节点1，所以$n_{54}^1=1,g_{54}=1$

从5->3,最短路径为（5，3），该路径不经过节点1，所以$n_{53}^1=0,g_{53}=1$

从5->2，最短路径为（5，1，2），（5，3，2），经过节点1的路径为（5，1，2），所以$n_{52}^1=1,g_{52}=2$

从4->3,最短路径为（4，1，2，3），（4，1，5，3），两条路径都经过节点1，所以$n_{43}^1=g_{43}^1=2$

从4->2,最短路径为（4，1，2），该路径经过节点1，所以$n_{42}^1=g_{42}^1=1$

从3->2,最短路径为（3，2），该路径不经过节点1，所以$n_{32}^1=0,g_{32}^1=1$

综上，得出结论：$B(1)=\frac{1}{1}+\frac{0}{1}+\frac{1}{2}+\frac{2}{2}+\frac{1}{1}+\frac{0}{1}=\frac{7}{2}$；利用（4）式归一化得$B(1)=\frac{7}{12}$。



