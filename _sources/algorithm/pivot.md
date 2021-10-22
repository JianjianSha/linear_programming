# 转轴操作

考虑以下线性方程组

$$\mathbf y^{\top}A=\mathbf s^{\top}$$ (pivot1)

其中 $\mathbf y^{\top}=(y_1,\cdots,y_m)$，$\mathbf s^{\top}=(s_1,\cdots, s_n)$ ，且

$$A=\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\
a_{21} & a_{22} & \cdots & a_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}$$

$\mathbf s$ 是因变量向量，其依赖于独立变量向量 $\mathbf y$，假设我们交换一个因变量与一个独立变量，例如 $s_j$ 和 $y_i$，那么只要 $a_{ij}\neq 0$，这种交换就可以实现，求 $y_i$ 的表达式

$$y_i=\frac 1 {a_{ij}}(-y_1a_{1j}-\cdots-y_{i-1}a_{(i-1)j}+s_j-y_{i+1}a_{(i+1)j}-\cdots-y_m a_{mj})$$ (pivot2)

代入方程组各等式，得

$$y_1\left(a_{1k}-\frac {a_{ik}a_{1j}}{a_{ij}}\right)+\cdots+s_j\left(\frac {a_{ik}}{a_{ij}}\right)+\cdots +y_m\left(a_{mk}-\frac {a_{ik}a_{mj}}{a_{ij}}\right)=s_k$$ (pivot3)

显然当 $k=j$ 时，上式变为 $s_j=s_j$，这是因为经过交换后， $s_j$ 变成独立变量，所以第 $j$ 个等式由 {eq}`pivot2` 给出。将交换后的方程组展开显示如下

$$\begin{matrix} y_1 \hat a_{11}+\cdots+s_j  \hat a_{i1}+\cdots + y_m \hat a_{m1}= s_1 \\
 \vdots \\
 y_1\hat a_{1j}+\cdots+s_j  \hat a_{ij}+\cdots + y_m \hat a_{mj}= y_i \\
\vdots \\
y_1\hat a_{1n}+\cdots+s_j  \hat a_{in}+\cdots + y_m \hat a_{mn}= s_n
\end{matrix}$$

每个等式对应新的参数矩阵 $\hat A$ 的一列，$\hat A$ 可根据 {eq}`pivot2` 和 {eq}`pivot3` 式得到，观察可知，第 $i$ 行和第 $j$ 列比较特殊，故分四种情况：

$$\begin{aligned} \hat a_{ij} &=\frac 1 {a_{ij}}\\
\hat a_{hj}&=-\frac {a_{hj}}{a_{ij}} \quad h\neq i\\
\hat a_{ik}&=\frac {a_{ik}}{a_{ij}} \quad k \neq j\\
\hat a_{hk}&=a_{hk}-\frac {a_{ik}a_{hj}}{a_{ij}} \quad k\neq j, h \neq i
\end{aligned}$$

使用表格展示这一变换过程，

$$\begin{array}{c|ccccc|}
& s_1 & \cdots& s_j &\cdots& s_n \\
\hline
y_1 & a_{11}&\cdots &a_{1j}&\cdots& a_{1n}\\
\vdots & \vdots & & \vdots && \vdots\\
y_i & a_{i1} & \cdots & [a_{ij}] & \cdots & a_{in}\\
\vdots & \vdots & & \vdots && \vdots \\
y_m & a_{m1} & \cdots & a_{mj} & \cdots & a_{mn}\\
\hline
\end{array}
\quad 
\longrightarrow
\quad 
\begin{array}{c|ccccc|}
& s_1 & \cdots& y_i &\cdots& s_n \\
\hline
y_1 & \hat a_{11}&\cdots &\hat a_{1j}&\cdots& \hat a_{1n}\\
\vdots & \vdots & & \vdots && \vdots\\
s_j & \hat a_{i1} & \cdots & \hat a_{ij} & \cdots & \hat a_{in}\\
\vdots & \vdots & & \vdots && \vdots \\
y_m & \hat a_{m1} & \cdots & \hat a_{mj} & \cdots & \hat a_{mn}\\
\hline
\end{array}$$

称 $a_{ij}$ 为转轴点（pivot），在上面左侧表格，我们将转轴点 $a_{ij}$ 用方框标出，

总结上面四种情况的系数操作：

1. 转轴点位置：取倒数
2. 与转轴点同一列：取相反数，然后再除以转轴点的系数
3. 与转轴点同一行：除以转轴点系数
4. 其他位置：将此位置分别映射到转轴点所在的行和列，取两个映射位置上的系数的乘积，再除以转轴点系数，最后从此位置的系数中减去刚才得到的商。

用符号表示则为

$$\begin{array}{|lr|}
\hline
[p] & r \\
c & q \\
\hline
\end{array}
\quad
\longrightarrow
\quad
\begin{array}{|lr|}
\hline
1/p & r/p \\
-c/p & q-(rc/p) \\
\hline
\end{array}$$

# 例子

$$\begin{array}{c|ccc|}
& s_1 & s_2& s_3 \\
\hline
y_1 & 3 & 1 & 5\\
y_2 & [2]  & -3 & 1\\
y_3 & 0 & 3 & 1\\
\hline
\end{array}

\quad
\longrightarrow
\quad
\begin{array}{c|ccc|}
& y_2 & s_2& s_3 \\
\hline
y_1 & -3/2 & 11/2 & 7/2\\
s_1 & 1/2  & -3/2 & 1/2\\
y_3 & 0 & 3 & [1]\\
\hline
\end{array}
\quad
\longrightarrow
\quad \cdots$$

如果将 $y_1, \ y_2, \ y_3$ 全部与 $s_1, \ s_2, \ s_3$ 进行交换，那么最后得到的 $\hat A=A^{-1}$，这是因为 $\mathbf y^{\top}=\mathbf s^{\top} A^{-1}=\mathbf s^{\top} \hat A$ ，这种方法可以求 $A^{-1}$，当然前提条件是矩阵是方阵，且全部转轴点的元素值非 0 。
