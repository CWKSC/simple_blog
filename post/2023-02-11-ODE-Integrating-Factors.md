上一篇： [Separable, Homogeneous, Exact Equations](post\2023-02-04-ODE-Separable-Homogeneous-Exact-Equations.md)

# Integrating Factors 積分因子

若果 $M(x, y) dx + N(x, y) dy = 0$ 中

$$
\frac{\partial M}{\partial y} \not= \frac{\partial N}{\partial x}
$$

（Not Exact 不恰當，因此無法用恰當方程式的方法去解）

而存在一個非零函數 $\mu(x, y)$ ，令 

$$
(\mu M) dx + (\mu N) dy = 0
$$

為 Exact 恰當， $\mu(x, y)$ 則稱為 Integrating Factors 積分因子

有至少以下六種方法求 $\mu(x, y)$ 積分因子：

## 方法一（常用）

若

$$
\frac{1}{N} (\frac{\partial M}{\partial y} - \frac{\partial N}{\partial x})
$$

只包括 x ，則

$$
\mu = e^{\int \frac{1}{N} (\frac{\partial M}{\partial y} - \frac{\partial N}{\partial x}) dx}
$$

若

$$
\frac{1}{M} (\frac{\partial N}{\partial x} - \frac{\partial M}{\partial y})
$$

只包括 y ，則

$$
\mu = e^{\int \frac{1}{M} (\frac{\partial N}{\partial x} - \frac{\partial M}{\partial y}) dy}
$$

### 方法一的證明

由於 $(\mu M) dx + (\mu N) dy = 0$ 為恰當

$$
\frac{\partial}{\partial y} [\mu(x, y) M(x, y)] = \frac{\partial}{\partial x} [\mu(x, y) N(x, y)] \\
$$

假設 $\mu(x, y)$ 只包括 x，即 $\mu(x)$ ，則

$$
\begin{align}
\frac{\partial \mu(x)}{\partial x} &= \frac{d \mu(x)}{d x} \\
\frac{\partial \mu(x)}{\partial y} &= 0
\end{align}
$$

上面的公式轉變為

$$
\frac{\partial}{\partial y} [\mu(x) M(x, y)] = \frac{\partial}{\partial x} [\mu(x) N(x, y)] \\
$$

用 乘法法則 (Product Rule for Derivatives) 展開

$$
\begin{align}
\frac{\mu(x)}{\partial y} M(x, y) + \mu(x) \frac{\partial M(x, y)}{\partial y} &= \frac{\partial \mu(x)}{\partial x} N(x, y) + \mu(x) \frac{\partial N(x, y)}{\partial x} \\
0 + \mu(x) \frac{\partial M(x, y)}{\partial y} &= \frac{d \mu(x)}{d x} N(x, y) + \mu(x) \frac{\partial N(x, y)}{\partial x} \\
\mu(x) \frac{\partial M(x, y)}{\partial y} - \mu(x) \frac{\partial N(x, y)}{\partial x} &= \frac{d \mu(x)}{d x} N(x, y) \\
\mu(x) (\frac{\partial M(x, y)}{\partial y} - \frac{\partial N(x, y)}{\partial x}) &= \frac{d \mu(x)}{d x} N(x, y) \\
\frac{1}{N(x, y)} (\frac{\partial M(x, y)}{\partial y} - \frac{\partial N(x, y)}{\partial x}) &= \frac{1}{\mu(x)} \frac{d \mu(x)}{d x} \\
\frac{1}{N(x, y)} (\frac{\partial M(x, y)}{\partial y} - \frac{\partial N(x, y)}{\partial x}) dx &= \frac{1}{\mu(x)} d \mu(x) \\
\int \frac{1}{N(x, y)} (\frac{\partial M(x, y)}{\partial y} - \frac{\partial N(x, y)}{\partial x}) dx &= \int \frac{1}{\mu(x)} d \mu(x) \\
\int \frac{1}{N(x, y)} (\frac{\partial M(x, y)}{\partial y} - \frac{\partial N(x, y)}{\partial x}) dx &= \ln \mu(x) \\
\mu(x) &= e^{\int \frac{1}{N(x, y)} (\frac{\partial M(x, y)}{\partial y} - \frac{\partial N(x, y)}{\partial x}) dx} \\
\end{align}
$$

同理

$$
\mu(y) = e^{\int \frac{1}{M(x, y)} (\frac{\partial N(x, y)}{\partial x} - \frac{\partial M(x, y)}{\partial y}) dy} \\
$$

### 例題 1：

求 $(x^2 + y^2 + x) dx + xy dy$ 的積分因子

$$
\begin{align}
\frac{\partial M}{\partial y} &= 2y \\
\frac{\partial N}{\partial x} &= y \\
\frac{1}{N} (\frac{\partial M}{\partial y} - \frac{\partial N}{\partial x} ) &= \frac{1}{xy} (2y - y) \\
&= \frac{1}{xy} y \\
&= \frac{1}{x} \\
\mu(x) &= e^{\int \frac{1}{x} dx} \\
&= e^{ln(x)} \\
&= x
\end{align}
$$

### 例題 2：

求 $(y^2 - 6xy) dx + (3xy - 6x^2) dy$ 的積分因子

$$
\begin{align}
\frac{\partial M}{\partial y} &= 2y - 6x \\
\frac{\partial N}{\partial x} &= 3y - 12x \\
\frac{1}{M} (\frac{\partial N}{\partial x} - \frac{\partial M}{\partial y} ) &= \frac{3y - 12x - 2y + 6x}{y^2 - 6xy}  \\
&= \frac{y - 6x}{y (y - 6x)} \\
&= \frac{1}{y} \\
\mu(y) &= e^{\int \frac{1}{y} dx} \\
&= e^{ln(y)} \\
&= y
\end{align}
$$

## 方法二

若

$$
M(x, y) dx + N(x, y) dy = 0
$$

為 Homogeneous Equations 齊次方程式

當 $xM + yN \not = 0$ 時，則

$$
\mu = \frac{1}{xM + yN}
$$

當 $xM + yN = 0$ 時，則 

$$
\mu = \frac{1}{xy}
$$

## 方法三

若

$$
\frac{\partial M}{\partial y} - \frac{\partial N}{\partial x} = f(xy)(Mx - Ny)
$$

則

$$
\mu = e^{-\int f(xy) d(xy)}
$$

## 方法四

若 $M(x, y) dx + N(x, y) dy = 0$ 可改寫為

$$
yf(xy) dx + x g(xy) dy
$$

的形式，其中 $f(xy) \not = g(xy)$

則

$$
\mu = \frac{1}{xM-yN}
$$

## 方法五（這個不知道誰會用）

若微分方程式可改寫為

$$
x^ay^b(C_1 y dx + C_2 x dy) + x^c y^d (C_3 y dx + C_4 x dy) = 0
$$

其中 $C_1  C_4 \not = C_2 C_3$ 

則 $\mu$ 會是 $x^m y^n$ 的形式 （只是形式，不是解）

## 方法六

查表
