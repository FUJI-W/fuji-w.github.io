### NeRF渲染方程求导

由前面的推导，我们得到了NeRF的渲染方程的离散表达：

$$
L(\mathbf{x},\omega)=L(s)=\sum_{n=1}^{N}C_nT_n(1-e^{-\sigma_n\delta_n}),\quad T_n=e^{-\sum_{k=1}^{n-1}\sigma_k\delta_k}
$$

下面我们分别推导该渲染方程在采样点 $t$ 处的关于颜色强度与吸收系数的导数计算式。

#### 关于颜色强度的导数

$$
\frac{\partial{L(\mathbf{x},\omega)}}{\partial{C_t}}
=
\frac{\partial(\sum_{n=1}^{N}C_nT_n(1-e^{-\sigma_n\delta_n}))}{\partial{C_t}}
=T_t(1-e^{-\sigma_t\delta_t})
$$

#### 关于吸收系数的导数

$$
\begin{aligned}
\frac{\partial{L(\mathbf{x},\omega)}}{\partial{\sigma_t}}
&=\frac{\partial{(\sum_{n=1}^{N}C_nT_n(1-e^{-\sigma_n\delta_n}))}}{\partial{\sigma_t}}\\
&=\sum_{n=t}^{N}C_n\frac{\partial{(T_n(1-e^{-\sigma_n\delta_n}))}}{\partial{\sigma_t}}\\
&=\sum_{n=t}^{N}C_nT_n\frac{\partial{(1-e^{-\sigma_n\delta_n})}}{\partial{\sigma_t}}
+\sum_{n=t}^{N}C_n\frac{\partial{T_n}}{\partial{\sigma_t}}(1-e^{-\sigma_n\delta_n})\\
&=C_tT_te^{-\sigma_t\delta_t}\delta_t
+\sum_{n=t+1}^{N}C_n\frac{\partial{T_n}}{\partial{\sigma_t}}(1-e^{-\sigma_n\delta_n})
\end{aligned}
$$

进一步地：

$$
\begin{aligned}
\frac{\partial{T_n}}{\partial{\sigma_t}}
&=\frac{\partial{(e^{-\sum_{k=1}^{n-1}\sigma_k\delta_k}})}{\partial{\sigma_t}}\\
&=\frac{\partial{(e^{-\sum_{1}^{t-1}\sigma_k\delta_k}e^{-\sum_{t+1}^{n}\sigma_k\delta_k}}e^{-\sigma_t\delta_t})}{\partial{\sigma_t}}\\
&=\frac{\partial{(T_tT_{t+2\to n}e^{-\sigma_t\delta_t})}}{\partial{\sigma_t}}\\
&=-T_tT_{t+2\to n}e^{-\sigma_t\delta_t}\delta_t\\
&=-T_n\delta_t
\end{aligned}
$$

代入到前式可得，渲染方程关于吸收系数的导数的表达式为：

$$
\begin{aligned}
\frac{\partial{L(\mathbf{x},\omega)}}{\partial{\sigma_t}}
&=C_tT_te^{-\sigma_t\delta_t}\delta_t
-\sum_{n=t+1}^{N}C_nT_n(1-e^{-\sigma_n\delta_n})\delta_t\\
\end{aligned}
$$

最后，若直接使用上式计算，在求解 $t$ 点的导数时还需要遍历 $t$ 点之后的采样点，计算成本较高。考虑到在实际求解过程中，导数计算是在正向渲染之后进行的，即最终的渲染结果 $L(\mathbf{x},\omega)$ 已知，所以一般在实际应用中，会对上式作进一步地转换，得到最终的计算式：

$$
\begin{aligned}
\frac{\partial{L(\mathbf{x},\omega)}}{\partial{\sigma_t}}
&=C_tT_te^{-\sigma_t\delta_t}\delta_t
-[L(\mathbf{x},\omega)-\sum_{n=1}^{t}C_nT_n(1-e^{-\sigma_n\delta_n})]\delta_t\\
&=C_tT_{t+1}\delta_t-[L(\mathbf{x},\omega)-\sum_{n=1}^{t}C_nT_n(1-e^{-\sigma_n\delta_n})]\delta_t
\end{aligned}
$$
