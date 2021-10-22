# 单纯形法

## 疯狂转轴法
考虑标准最小化问题，求 $\mathbf y$ 使得 $\mathbf y^{\top}\mathbf b$ 最小，且满足 $\mathbf y \ge \mathbf 0$ 以及 $\mathbf y^{\top}A \ge \mathbf c^{\top}$ 。

将最后一个约束关系集的不等关系改成等式关系，为此，增加松弛变量 $\mathbf s$，使得 $\mathbf s^{\top}=\mathbf y^{\top}A - \mathbf c^{\top} \ge \mathbf 0$，并给出如下表格以表示这个松弛变量与目标变量的关系，

$$\begin{array} {c|cccc|c} 
& s_1 & s_2 & \cdots & s_n\\
\hline
y_1& a_{11} & a_{12} & \cdots & a_{1n} & b_1\\
y_2& a_{21} & a_{22} & \cdots & a_{2n} & b_2\\
\vdots & \vdots & \vdots & & \vdots & \vdots\\
y_m& a_{m1} & a_{m2} & \cdots & a_{mn} & b_m\\
\hline
1 & -c_1 & -c_2 & \cdots & -c_n & 0
\end{array}$$
<center>单纯形表</center>

最后一列表示向量 $\mathbf b$ 与 $\mathbf y$ 的内积，是我们需要最小化的目标（其实也可以写在表中右上角位置）。

如果 $-\mathbf c \ge \mathbf 0$，并且 $\mathbf b \ge 0$ （对应上表中，**最后一行和最后一列全部非负**），那么根据约束条件 $\mathbf y \ge \mathbf 0$，有 $\mathbf y^{\top}\mathbf b \ge 0$，在 $\mathbf y=\mathbf 0$ 处取得最小值 $0$，另外一方面，$\mathbf y=\mathbf 0$ 满足 $\mathbf s^{\top}=\mathbf y^{\top}A - \mathbf c^{\top}=- \mathbf c^{\top} \ge \mathbf 0$，即所有约束条件均得到满足，故 $\mathbf y=\mathbf 0$ 时，目标取得最小值 $0$ 。

但是如果最后一行或者最后一列中存在负值，那么就无法轻易的得到最优解了。利用前面所讨论的转轴操作，我们选取某个转轴点，例如 $a_{11}$（假设 $a_{11}\neq 0$），包括最后一行和最后一列也参与转轴操作，结果如下表

$$\begin{array} {c|cccc|c} 
& y_1 & s_2 & \cdots & s_n\\
\hline
s_1& \hat a_{11} & \hat a_{12} & \cdots & \hat a_{1n} & \hat b_1\\
y_2& \hat a_{21} & \hat a_{22} & \cdots & \hat a_{2n} & \hat b_2\\
\vdots & \vdots & \vdots & & \vdots & \vdots\\
y_m& \hat a_{m1} & \hat a_{m2} & \cdots & \hat a_{mn} & \hat b_m\\
\hline
1 & -\hat c_1 & -\hat c_2 & \cdots & -\hat c_n & \hat v
\end{array}$$

令 

$$\mathbf r = (r_1,\cdots r_n)=(y_1,s_2,\cdots, s_n)\\
\mathbf t=(t_1,\cdots, t_m)=(s_1,y_2,\cdots, y_m)$$ (simp1)

根据转轴操作的定义，相关的方程组等式关系保持不变，所以原来的 $\mathbf s^{\top}=\mathbf y^{\top}A-\mathbf c^{\top}$ 等价于 $\mathbf r^{\top}=\mathbf t^{\top}\hat A-\hat {\mathbf c}$，优化目标为 $\sum_{i=1}^m y_i b_i=y_1b_1+\sum_{i=2}^m y_i b_i$，将 $y_1$ 用 $\mathbf t$ 表示为 $y_1=\mathbf t^{\top} \hat A_{:,1}-\hat c_1$，展开得

$$y_1=\frac 1 {a_{11}}s_1-\frac {a_{21}}{a_{11}}y_2-\cdots - \frac {a_{m1}}{a_{11}}y_m+\frac {c_1}{a_{11}}$$

于是目标函数为

$$\sum_{i=1}^m y_i b_i=\frac {b_1} {a_{11}}s_1+(b_2-\frac {a_{21}b_1}{a_{11}})y_2+\cdots +(b_m- \frac {a_{m1}b_1}{a_{11}})y_m+\frac {c_1b_1}{a_{11}}=\mathbf t^{\top}\hat {\mathbf b}+\hat v$$

经过转轴操作后，问题转变为：求 $\mathbf y$ 和 $\mathbf s$，使 $\mathbf t^{\top}\hat {\mathbf b}$ 最小（$\hat v$ 与 $\mathbf y$ 和 $\mathbf s$ 均无关），且满足 $\mathbf y, \ \mathbf s \ge \mathbf 0$ 以及 $\mathbf r=\mathbf t^{\top} \hat A - \hat {\mathbf c}$ ， $\mathbf {r,t}$ 的定义见 {eq}`simp1` 式。

根据 $\mathbf y, \ \mathbf s \ge \mathbf 0$ 和 $\mathbf {r,t}$ 的定义可知，$\mathbf r, \ \mathbf t \ge \mathbf 0$ ，故如果 $-\hat {\mathbf c} \ge \mathbf 0$ 且 $\hat {\mathbf b} \ge \mathbf 0$，那么很明显在 $\mathbf t=\mathbf 0$ 处 $\mathbf t^{\top}\hat {\mathbf b}$ 有最小值 $0$，此时 $\mathbf r=-\hat {\mathbf c}$，$\mathbf r$ 给定了最优解，原先的目标值为 $\mathbf y^{\top}\mathbf b=\hat v$ 。

**疯狂转轴法：** 一直转轴下去，直到最后一行和最后一列全部非负，此时设置左侧变量为 0，顶部变量的值为最后一行的元素值，这就是最优解，最优值则是右下角的元素值。

这个方法也可用于求解对偶问题：在满足 $\mathbf x \ge \mathbf 0$ 和 $A\mathbf x \le \mathbf b$ 的情况下最大化 $\mathbf c^{\top}\mathbf x$。为此，我们添加松弛变量 $\mathbf u = \mathbf b - A\mathbf x$，问题转变为求 $\mathbf x$ 和 $\mathbf u$ 使得 $\mathbf c^{\top}\mathbf x$ 最小，且同时满足 $\mathbf {x, u} \ge \mathbf 0$ 和 $\mathbf u=\mathbf b-A\mathbf x$ 。

将等式约束条件改写为 $-\mathbf u = A\mathbf x - \mathbf b$，那么单纯形表为

$$\begin{array} {c|cccc|c} 
& x_1 & x_2 & \cdots & x_n & -1\\
\hline
-u_1& a_{11} & a_{12} & \cdots & a_{1n} & b_1\\
-u_2& a_{21} & a_{22} & \cdots & a_{2n} & b_2\\
\vdots & \vdots & \vdots & & \vdots & \vdots\\
-u_m& a_{m1} & a_{m2} & \cdots & a_{mn} & b_m\\
\hline
 & - c_1 & -c_2 & & - c_n & 0
\end{array}$$

左下角位置为目标函数的相反数，相当于最小化 $-\mathbf c^{\top}\mathbf x$ 。

注意到，如果 $-\mathbf c \ge \mathbf 0$ 且 $\mathbf b \ge \mathbf 0$，那么 $-\mathbf c^{\top}\mathbf x \ge 0$，在 $\mathbf x=\mathbf 0$ 时有最小值 $0$，且此时满足约束条件 $\mathbf u=\mathbf b-A\mathbf x=\mathbf b \ge \mathbf 0$，故此时， $\mathbf x = \mathbf 0$ 是最优解。

如果最后一行和最后一列存在负值，那么进行转轴操作，例如选择转轴点 $a_{11}$（假设 $a_{11}\neq 0$），有

$$-x_1=\frac 1 {a_{11}}u_1+\frac {a_{12}}{a_{11}}x_2+\cdots+\frac {a_{1n}}{a_{11}}x_n-\frac {b_1}{a_{11}}\\
-u_2=-\frac {a_{21}}{a_{11}}u_1+(a_{22}-\frac {a_{21}a_{12}}{a_{11}})x_2+\cdots -(b_2-\frac {a_{21}b_1}{a_{11}})\\
\vdots$$

不难发现，变换规则与最小化问题中的转轴变换规则完全相同。如果变换之后最后一行和最后一列全部非负，那么仿照 {eq}`simp1`， 定义
$$\mathbf r = (r_1,\cdots r_n)=(u_1,x_2,\cdots, x_n)\\
\mathbf t=(t_1,\cdots, t_m)=(x_1,u_2,\cdots, u_m)$$

此时的原目标（这里将目标函数乘以 $-1$ 从而改成了最小化）为

$$\begin{aligned}-\mathbf c^{\top}\mathbf x &=-c_1x_1-\sum_{j=2}^n c_j x_j\\
&=\left[\frac {c_1}{a_{11}}u_1+(\frac {a_{12}c_1}{a_{11}}-c_2)x_2+\cdots + (\frac {a_{1n}c_1}{a_{11}}-c_n)x_n\right] - \frac {b_1c_1}{a_{11}}\\
&=-\hat{\mathbf c}^{\top}\mathbf r-\hat v
\end{aligned}$$

注意，将 $(-\hat {\mathbf c})$ 看作一个整体，为最后一行的元素向量，根据假设“变换之后最后一行和最后一列全部非负”，即 $-\hat {\mathbf c} \ge \mathbf 0$，以及 $\hat {\mathbf b} \ge \mathbf 0$，那么 $-\hat {\mathbf c}^{\top}\mathbf r \ge 0$，在 $\mathbf r=\mathbf 0$ 处取得最小值，此时 $\mathbf t=\hat {\mathbf b} - \hat A \mathbf r=\hat {\mathbf b} \ge \mathbf 0$ 满足约束条件。

上式中 $\hat v$ 为右下角元素变换后的值，$\hat v$ 与 $\mathbf {x, u}$ 无关，所以 $-\hat {\mathbf c}^{\top}\mathbf r$ 取最小值 $0$ 时，原目标 $-\mathbf c^{\top}\mathbf x$ 有最小值 $-\hat v$，即 $\mathbf c^{\top}\mathbf x$ 有最大值 $\hat v$ ，最优解为 $\mathbf t=\hat {\mathbf b} - \hat A \mathbf r=\hat {\mathbf b}$ 。

持续进行转轴操作，直到最后一行和最后一列全部非负，此时 **顶部变量全部为 0，左侧变量值等于最后一列的值（注意不是左侧元素，左侧元素值为最右列元素值乘以 $-1$），目标最优值为右下角的元素值，最优解为最右列元素值**。

将 $-u_i$ 看作 $y_i$，那么就得到原最大化问题的对偶问题，即最小化问题，整个转轴操作求目标最优值与本文开头所讨论的最小化问题的方法完全一致，所以有如下总结。

## 总结
无论是最小化还剩最大化问题，均可以写出如下单纯形表，

$$\begin{array} {c|cccc|c} 
& x_1 & x_2 & \cdots & x_n & -1\\
\hline
y_1& a_{11} & a_{12} & \cdots & a_{1n} & b_1\\
y_2& a_{21} & a_{22} & \cdots & a_{2n} & b_2\\
\vdots & \vdots & \vdots & & \vdots & \vdots\\
y_m& a_{m1} & a_{m2} & \cdots & a_{mn} & b_m\\
\hline
1 & -c_1 & -c_2 & \cdots & -c_n & 0
\end{array}$$

然后一直进行转轴操作，直到最后一行和最后一列全部非负。目标最优值位于右下角元素的值。对于最小化问题，将最左一列的变量值 置 0，最上一行的变量值 取最下一行对应的元素值。对于最大化问题，将最上一行的变量值 置 0，最左一列的变量值 取最右一列对应元素的置。

## 例子

最大化目标 $5x_1+2x_2+x_3$，同时需要满足所有 $x_j \ge 0$ 以及

$$\begin{aligned} x_1+3x_2-x_3 & \le 6\\
x_2+x_3 & \le 4\\
3x_1+x_2 & \le 7\end{aligned}$$

对偶问题为：最小化 $6y_1+4y_2+7y_3$，且使得所有 $y_i \ge 0$ 以及

$$\begin{aligned} y_1+3x_3 & \ge 5\\
3y_1+y_2+x_3 & \ge 2\\
-y_1+y_2 & \ge 1\end{aligned}$$

写出单纯形表为

$$\begin{array} {c|ccc|c} 
& x_1 & x_2 & x_3 & \\
\hline
y_1& 1 & 3 & -1 & 6\\
y_2& 0 & 1 & [1] &4\\
y_3& [3] & 1 & 0 & 7\\
\hline
1 & -5 & -2 & -1 & 0
\end{array}
\quad \longrightarrow \quad
\begin{array} {c|ccc|c} 
& y_3 & x_2 & y_2 & \\
\hline
y_1&  &  &  & 23/3\\
x_3&  &  &  &4\\
x_1&  &  &  & 7/3\\
\hline
1 & 5/3 & 2/3 & 1 & 47/3
\end{array}$$

依次交换 $y_2 \leftrightarrow x_3$ 和 $y_3 \leftrightarrow x_1$，得到右侧表。最大化问题的最优解为 $x_1=7/3, \ x_2=0, \ x_3=4$（顶部向量为 $\mathbf 0$，左侧向量等于右侧值），目标最优值为 $47/3$ 。 对于最小化问题，最优解为 $y_1=0, \ y_2=1, \ y_3=5/3$（左侧向量为 $\mathbf 0$，顶部向量等于底部值），目标最优值依然为 $47/3$ 。