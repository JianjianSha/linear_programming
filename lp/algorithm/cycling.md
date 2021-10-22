# 循环

根据前面 单纯形法的转轴规则，如果所选转轴点的所在行最后一个元素 $b_{i_0}=0$，那么转轴操作并没有带来多少进展，即 $\hat b_k \ge b_k$ 中等号成立。实际上，很有可能经过一系列的转轴操作后，单纯形表回到最初状态。这就导致死循环。

**词典顺序**

给定两个不相等的 n-dim 向量 $\mathbf r \neq \mathbf s$，称 $\mathbf r$ 按词典顺序地小于 $\mathbf s$，记作 $\mathbf r \prec \mathbf s$，如果：$\mathbf {r, s}$ 中第一个不相等的元素有 $r_k < s_k$，其中 $r_1=s_1,\cdots, r_{k-1}=s_{k-1}$ 。

例如 $(0,3,2,3) \prec (1,2,2,-1) \prec (1,3,-100,-2)$ 。

## 避免循环

在单纯形表中 b 列的右侧增加一个 m 阶单位矩阵，在 $-\mathbf c$ 行 元素 $v$ 的右侧增加一个向量 $(c_{n+1},\cdots, c_{n+m})$，此向量初始为 $\mathbf 0$ 。单纯形表如下

$$\begin{array} {c|cccc|ccccc}
& x_1 & x_2 & \cdots & x_n & \\
\hline \\
y_1 & a_{11} & a_{12} & \cdots & a_{1n} & b_1 & 1 & 0 & \cdots & 0\\
y_2 & a_{21} & a_{22} & \cdots & a_{2n} & b_2 & 0 & 1 & \cdots & 0\\
\vdots & \vdots & \vdots & & \vdots & \vdots & & & \vdots \\
y_m & a_{m1} & a_{m2} & \cdots & a_{mn} & b_m & 0 & 0 & \cdots & 1\\
\hline \\
& -c_1 & -c_2 & \cdots & -c_n & v & c_{n+1} & c_{n+2} & \cdots & c_{n+m} 
\end{array}$$

记 $\mathbf b_1=(b_1,1,0,\cdots,0), \ldots, \mathbf b_m=(b_m,0,0,\cdots, 1)$，$\mathbf v = (v,c_{n+1},\cdots, c_{n+m})$ 。使用与之前相同的转轴规则，但是使用 $\mathbf b_i$ 代替 $b_i$，并使用词典顺序比较。

