# Linear First Order Differential Equations 線性一階微分方程式

線性微分方程式形式如下：

$$
y' + P(x)y = Q(x)
$$

若 $Q(x) = 0$ 則稱為線性齊次微分方程式，通解：

$$
y = C e^{-\int P(x) \, dx}
$$


若 $Q(x) \neq 0$ 則稱為線性非齊次微分方程式，通解：

$$
y = e^{-\int P(x) \, dx} \left[ \int Q(x) e^{\int P(x) dx} dx + C \right]
$$

## 線性齊次微分方程式 公式推導

由於 $Q(x) = 0$

$$
y' + P(x)y = 0
$$

用分離變數法

$$
\begin{align}
\frac{dy}{dx} &= - P(x) y \\
\frac{dy}{y} &= - P(x) dx \\
ln(y) &= - \int P(x) dx + C \\
y &= Ce^{- \int P(x) dx}
\end{align}
$$

## 線性非齊次微分方程式 公式推導

$$
\begin{align}
y' + P(x)y &= Q(x) \\
\frac{dy}{dx} &= Q(x) - P(x) y \\
(P(x) y - Q(x))dx + dy &= 0
\end{align}
$$

$$
\begin{align}
\frac{\partial M}{\partial y} &= P(x) \\
\frac{\partial N}{\partial x} &= 0 \\
\frac{\partial M}{\partial y} &\not = \frac{\partial N}{\partial x} 
\end{align}
$$

無法使用 Exact Equations 恰當方程式，需要求 Integrating Factors 積分因子 $\mu(x)$

$$
\begin{align}
&\frac{1}{N}(\frac{\partial M}{\partial y} - \frac{\partial N}{\partial x}) \\
& = \frac{1}{1} (P(x) - 0) \\
& = P(x) 
\end{align}
$$

$$
\mu(x) = e^{\int P(x) dx}
$$

$$
e^{\int P(x) dx} \left[ P(x)y - Q(x) \right] dx + e^{\int P(x) dx} dy = 0
$$

轉變為恰當方程式，求 Potential Function 位勢函數：

$$
\begin{align}
F &= \int M dx + k(y) \\
&= \int e^{\int P(x) dx} [ P(x) y - Q(x) ] dx + k(y) \\
&= y \int e^{\int P(x) dx} d (\int P(x) dx) - \int Q(x) e^{\int P(x) dx} dx + k(y) \\
&= y e^{\int P(x) dx} - \int Q(x) e^{\int P(x) dx} dx + k(y) \\
F &= \int N dy + k(x) \\
&= \int e^{\int P(x) dx} d y + k(x) \\
&= y e^{\int P(x) dx} + k(x) + C
\end{align}
$$

聯立兩條方程式

$$
\left\{
    \begin{matrix}
        F &=& y e^{\int P(x) dx} - \int Q(x) e^{\int P(x) dx} dx + k(y)\\
        F &=& y e^{\int P(x) dx} + k(x) + C
    \end{matrix}
\right.
$$

從第二條方程式可知，F 不含 y 變量，故 k(y) = 0

比較兩式， $k(y) = - \int Q(x) e^{\int P(x) dx} dx + C$

$$
\begin{align}
F &= C \\
y e^{\int P(x) dx} - \int Q(x) e^{\int P(x) dx} dx + C &= C \\
y e^{\int P(x) dx} = \int Q(x) e^{\int P(x) dx} dx + C 
\end{align}
$$

$$
y = e^{- \int P(x) dx} \left[ \int Q(x) e^{\int P(x) dx} dx + C \right]
$$

