# Ordinary Differential Equation (O.D.E) 常微分方程

## Content 內容:

- Separable Equation 可分離方程式 / 分離變數法

- Homogeneous Equations 齊次方程式

- Exact Equations 恰當方程式

## Order and Degree 階與次

Order 階是指 $\frac{dy}{dx}$ 的最高階數， $\frac{dy}{dx}$ 是一階， $\frac{d^2y}{dx^2}$ 是二階

Degree 次是指 $\frac{dy}{dx}$ 最高的冪數， $\frac{dy}{dx}$ 是一次， $\frac{dy}{dx}^2$ 是二次

## Solution form 解答形式

依型態可分為：

- Expilcit Solution 顯解

- Implicit Solution 隱解

依意義可分為：

- General Solution 通解

- Particular Solution 特解

- Singular Solution 奇異解

## Separable Equation 可分離方程式 / 分離變數法

沒什麼特別，把變數分離到方程的兩邊

$$
F(x, y, y') = 0
$$
$$
g(y) dy = f(x) dx 
$$
$$
\int_{}^{}g(y)dy = \int_{}^{}f(x)dx 
$$

例題1：

$$
\begin{align} 
x \frac{dy}{dx} &= 5y \\
x dy &= 5 y dx \\
\frac{1}{y} dy &= \frac{5}{x} dx \\
\int \frac{dy}{y} &= 5 \int \frac{dx}{x} \\
ln y &= 5 ln x + C \\
y &= Cx^5
\end{align}
$$

例題2：

$$
\begin{align} 
y' &= ay \\
\frac{dy}{y} &= a dx \\
ln y &= ax + C \\
y &= Ce^{ax}
\end{align}
$$

例題3：

$$
\begin{align} 
y' + ay + b &= 0 \text{, where } a \not= 0 \\
dy &= -(ay + b) dx \\
\frac{dy}{y + \frac{b}{a}} &= -a dx \\
ln(y + \frac{b}{a}) &= -a x + C \\
y &= Ce^{-ax} - \frac{b}{a}
\end{align}
$$

## Homogeneous Equations 齊次方程式

若 $f(\lambda x, \lambda y) = \lambda^m f(x, y)$ ，則稱 $f(x, y)$ 為 $m$ 次齊次

若一階微分方程式可以以下形式表示：

$$
M(x, y) dx + N(x, y) dy = 0
$$

當中 $M(x, y)$ $N(x, y)$ 為同次齊次，則稱為 Homogeneous Differential Equaltions 齊次微分方程式

例題1:

Prove $f(x, y) = x^3 + 10 x^2 y + 3xy^2 + y^3$ is homogeneous of degree 3 三次齊次函數

$$
\begin{align} 
&f(\lambda x, \lambda y) \\
&= (\lambda x)^3 + 10(\lambda x)^2(\lambda y) + 3 (\lambda x) (\lambda y)^2 + (\lambda y)^3 \\
&= \lambda^3 x^3 + 10 \lambda^3 x^2 y + 3 \lambda^3 x y^2 + \lambda^3 y^3 \\
&= \lambda^3 f(x, y)
\end{align}
$$

若果微分方程不能以 可分離方程式 / 分離變數法 求解

但本身為齊次微分方程式，即 $M(x, y) dx + N(x, y) dy = 0$

這種形式的方程可經過代換成為可分離，做法如下：

$dx$ 前面的函數 $M(x, y)$ 較簡單，$ \text{Let } x = vy, dx = v dy + y dv$

$dy$ 前面的函數 $N(x, y)$ 較簡單，$ \text{Let } y = ux, dy = u dx + x du$

例題1:

求解 $y dx = (2x + y) dy$

$$
\text{Let }x = vy, dx = vdy + y dv, v = \frac{x}{y}
$$

$$
\begin{align}
y(vdy + y dv) &= (2vy + y) dy \\
vdy + ydv &= (2v+1) dy \\
y dv &= (v + 1) dy \\
\frac{dv}{v + 1} &= \frac{dy}{y} \\
ln(v + 1) &= ln y + C\\
v + 1 &= Cy\\
\frac{x}{y} + 1 &= Cy\\
y + x &= C y^2
\end{align}
$$

## Exact Equations 恰當方程式

對於 $M(x, y) dx + N(x, y) dy = 0$ 

若 $\frac{\partial M}{\partial y} = \frac{\partial N}{\partial x}$ ，稱為 Exact 恰當

則存在 Potential Function 位勢函數 $F(x, y)$，當中：

$$
\partial F = \frac{\partial F}{\partial x} dx + \frac{\partial F}{\partial y} dy
$$

$$
\begin{align} 
\frac{\partial F}{\partial x} &= M & \frac{\partial F}{\partial y} &= N \\
F &= \int M dx + k(y) & F &= \int N dy + k(x)  \\
\frac{\partial F}{\partial y} &= \frac{\partial}{\partial y} [\int M dx + k(y)] & \frac{\partial F}{\partial x} &= \frac{\partial}{\partial x} [\int N dy + k(x)] \\
N &= \frac{\partial}{\partial y}[ \int M dx + k(y)] & M &= \frac{\partial}{\partial y}[ \int N dy + k(x)]
\end{align}
$$

例題1:

解 $xy' + y + 4 = 0$ 

改寫為 $M(x, y) dx + N(x, y) dy = 0$ 的形式

$$
\begin{align}
(y + 4) dx + x dy &= 0 \\
M(x, y) &= y + 4 \\
N(x, y) &= x
\end{align}
$$

$$
\text{Since } \frac{\partial M}{\partial y} = 1 = \frac{\partial N}{\partial x}, \text{It is exact} 
$$

M1 (Use $M(x, y)$ first, Then use $N(x, y)$ ):

$$
\begin{align}
F(x, y) &= \int M(x, y) dx + k(y) \\
F(x, y) &= \int (y + 4) dx + k(y) \\
&= x (y + 4) + k(y)\\
\text{Since } \frac{\partial F}{\partial y} &= N \\
\frac{\partial }{\partial y} [x(y + 4) + k(y)] &= x\\
x + k'(y) &= x \\
k'(y) &= 0 \\
k(y) &= C \\
F(x, y) &= x(y + 4) + C = C \\
x(y + 4) &= C 
\end{align}
$$
