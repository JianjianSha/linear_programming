# 简介

线性规划指 最大化/最小化 一个线性函数，且未知量满足一系列的线性约束条件，例如，最大化 $x_1+x_2$，其中约束条件为 $x_1, \ x_2\ge 0$，且

$$\begin{aligned}x_1+2x_2 & \le 4 \\
4x_1+2x_2 & \le 12 \\
-x_1+x_2 & \le 1 \end{aligned}$$ (lp1)

$\mathbf x=(x_1,x_2)$ 为要求的未知向量，这个例子中是二维情况，所以可以借助几何图形，直观地求解最优解，最优解为 $x_1=8/3, \ x_2=2/3$，但是对于高维，这个方法就不好处理了。

## 标准形式

标准最大化问题：求解 $\mathbf x \in \mathbb R^n$，使得

$$\begin{aligned} \max \ & \mathbf c^{\top} \mathbf x
\\ s.t. \ & A \mathbf x \le \mathbf b
\\ & \mathbf x \ge \mathbf 0
\end{aligned}$$ (lp2)

其中 $A \in \mathbb R^{m,n}, \ \mathbf b \in \mathbb R^m, \ \mathbf c \in \mathbb R^n$ 。

标准最小化问题：求解 $\mathbf y \in \mathbb R^m$，使得

$$\begin{aligned} \min \ & \mathbf y^{\top} \mathbf b
\\ s.t. \ &  \mathbf y^{\top}A \ge \mathbf c^{\top}
\\ & \mathbf y \ge \mathbf 0
\end{aligned}$$ (lp3)

其中 $A \in \mathbb R^{m,n}, \ \mathbf b \in \mathbb R^m, \ \mathbf c \in \mathbb R^n$ 。

## 对偶

### 定义

{eq}`lp2` 式所描述的最大化问题的对偶问题为 {eq}`lp3` 所描述的最小化问题，这两个线性规划问题共享参数$A \in \mathbb R^{m,n}, \ \mathbf b \in \mathbb R^m, \ \mathbf c \in \mathbb R^n$ 。

例如上面的 {eq}`lp1` 式问题，其对偶问题为：

$$\begin{aligned} \min \ & 4y_1+12y_2+y_3
\\ s.t. \ & y_1+4y_2-y_3 \ge 1
\\ & 2y_1+2y_2+y_3 \ge 1
\end{aligned}$$


```{note}
每个线性规划问题都有一个对偶线性规划问题，且这两个线性规划问题互为对偶。
```

将 {eq}`lp3` 的最小化问题的参数均乘以 $-1$，就可以转化为最大化问题，注意，对不等式两边取矩阵转置，不等号不变，

$$\begin{aligned} \max \ & (-\mathbf b^{\top}) \mathbf y
\\ s.t. \ &  (-A^{\top})\mathbf y\le -\mathbf c
\\ & \mathbf y \ge \mathbf 0
\end{aligned}$$

根据对偶的定义，可以得到这个最大化问题的对偶问题，

$$\begin{aligned} \min \ & \mathbf x^{\top} (-\mathbf c)
\\ s.t. \ & \mathbf x^{\top} (-A^{\top})\ge -\mathbf b^{\top}
\\ & \mathbf x \ge \mathbf 0
\end{aligned}$$

将参数分别乘以 $-1$，就可以将上述问题转换为最大化问题（当然，还需要两边进行转置），这与 {eq}`lp2` 完全相同。

### 性质

满足约束条件的解称为 **可行解**。下面考虑对偶的几个性质。

$\bigtriangleup$ **定理1：** 如果 $\mathbf x$ 是 {eq}`lp2` 的可行解，$\mathbf y$ 是 {eq}`lp3` 的可行解，那么有 

$$\mathbf c^{\top} \mathbf x \le \mathbf y^{\top} \mathbf b$$ (lp4)

证： 
$$\mathbf c^{\top} \mathbf x \le \mathbf y^{\top}A \mathbf x \le \mathbf y^{\top}\mathbf b$$

根据 {eq}`lp3`，$\mathbf c^{\top} \le \mathbf y^{\top}A$，当 $\mathbf x \ge 0$ 时，有第一个不等关系成立。（可以用一维情况帮助理解：当 $x\ge 0$ 时，固定 $x$ 值，$xz$ 是 $z$ 的增函数）

类似地 根据 {eq}`lp2`，可以得到第二个不等关系成立。$\Box$

$\bigtriangleup$ **结论1：** 互为对偶的两个标准问题均是可行的（指 可行集不为空），那么它们都是有界可行（指 目标函数在可行集上有界）。

证：令 $\mathbf y$ 是最小化问题的一个可行解，那么对于任意一个可行解 $\mathbf x$，根据 {eq}`lp4` 式可知最大化问题的目标函数有**上界**。类似地，可知最小化问题在可行集上有**下界**。$\Box$

$\bigtriangleup$ **结论2：** 如果 $\mathbf x^{\star}, \ \mathbf y^{\star}$ 分别是 {eq}`lp2` 和 {eq}`lp3` 式的可行解，且满足 $\mathbf c^{\top}\mathbf x^{\star}=\mathbf y^{\star \top}\mathbf b$，那么它们分别是各自问题的最优解。

证：令 $\mathbf x$ 是 {eq}`lp2` 的任意一个可行解，那么根据 {eq}`lp4` 式有 $\mathbf c^{\top}\mathbf x \le \mathbf y^{\star\top}\mathbf b=\mathbf c^{\top}\mathbf x^{\star}$，故 $\mathbf x^{\star}$ 是最优解。对称地可证 $\mathbf y^{\star}$ 是 {eq}`lp3` 式的最优解。$\Box$

$\bigtriangleup$ **对偶定理：** 如果一个标准线性规划问题是有界可行的，那么其对偶问题也是有界可行的，它们均存在最优解，且最优值相等。

证明有些复杂，留待以后再证。

$\bigtriangleup$ **均衡定理：** 如果 $\mathbf x^{\star}$ 和 $\mathbf y^{\star}$ 分别是 {eq}`lp2` 和 {eq}`lp3` 的可行解，那么它们分别是最优解当且仅当

对所有满足 $\sum_{j=1}^n a_{ij}x_j^{\star}<b_i$ 的 $i$ 有 

$$y_i^{\star}=0$$ (lp5)

并且，对所有满足 $\sum_{i=1}^m y_i^{\star}a_{ij}>c_i$ 的 $j$ 有 

$$x_j^{\star}=0$$ (lp6)

证：**当** 根据 {eq}`lp5` 式，只有满足 $\sum_{j=1}^n a_{ij}x_j^{\star}=b_i$ 的 $y_i^{\star} \neq 0$，

$$\sum_{i=1}^m y_i^{\star} b_i=\sum_{i=1}^m y_i^{\star} \sum_{j=1}^n a_{ij}x_j^{\star}=\sum_{i=1}^m\sum_{j=1}^n y_i^{\star} a_{ij} x_j^{\star}$$

类似地根据 {eq}`lp6` 式有，

$$\sum_{j=1}^n c_j x_j^{\star} =\sum_{i=1}^m\sum_{j=1}^n y_i^{\star} a_{ij} x_j^{\star}$$

再根据 结论 2，可得 $\mathbf x^{\star}, \mathbf y^{\star}$ 分别是 {eq}`lp2` 和 {eq}`lp3` 的最优解。

**仅当** 根据 定理 1 的证明，可知

$$\sum_{j=1}^n c_j x_j^{\star} \le \sum_{i=1}^m \sum_{j=1}^n y_i^{\star}a_{ij} x_j^{\star} \le \sum_{i=1}^m y_i^{\star}b_i$$

根据对偶定理，如果 $\mathbf x^{\star}$ 和 $\mathbf y^{\star}$ 是最优解，那么最优值相等即，上面不等式最左侧等于最右侧，也就是说，两个不等式中等式关系都成立， 于是有

$$\sum_{j=1}^n \left(c_j - \sum_{i=1}^m y_i^{\star} a_{ij}\right)x_j^{\star}=0$$ (lp7)

由于 $\mathbf x^{\star}$ 和 $\mathbf y^{\star}$ 是最优解，自然也是可行解，所以 $c_j - \sum_{i=1}^m y_i^{\star} a_{ij} \le 0$，当 $c_j - \sum_{i=1}^m y_i^{\star} a_{ij} = 0$ 时，{eq}`lp7` 式中对应的求和项（item） 为 0，所以就等价于 $c_j - \sum_{i=1}^m y_i^{\star} a_{ij}<0$ 对应的求和项相加，而 $x_j^{\star} \ge 0$，所以 $\left(c_j - \sum_{i=1}^m y_i^{\star} a_{ij}\right)x_j^{\star} \le 0$，要使得相加之和为 0，则必须每一项都为 0，故 $x_j^{\star}=0$，其中 $j$ 满足 $\sum_{i=1}^m y_i^{\star} a_{ij}>c_j$ 。类似地，可知，当 $\sum_{j=1}^n a_{ij}x_j^{\star}<b_i$ 时有 $y_i^{\star}=0$ 。$\Box$


{eq}`lp5` 和 {eq}`lp6` 式也称互补松弛条件。$x_j^{\star}>0$ 严格不等关系，使得 $x_j^{\star}$ 需要引入一个松弛变量，这意味着对偶问题中的相对应的互补约束条件可以取得等式关系 $\sum_{i=1}^m y_i^{\star} a_{ij} =c_j$。反过来讲，如果 $\sum_{i=1}^m y_i^{\star} a_{ij} >c_j$ 取严格不等，那么其对偶问题中的约束必然是 $x_j^{\star}=0$


