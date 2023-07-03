### 坐标系规定

#### film space coordinates

![image-20230610175724563](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202306101757066.png)
$$
\frac{x'}{x}=\frac{y'}{y}=\frac{f}{z} \quad \Rightarrow \quad 
\begin{pmatrix}x' \\ y' \\ 1\end{pmatrix}=\frac{1}{z}\begin{pmatrix}f & 0 & 0 \\ 0 & f & 0 \\ 0 & 0 & 1\end{pmatrix}\begin{pmatrix}x \\ y \\ z\end{pmatrix}
$$

#### screen space coordinates

##### 一般模型

![image-20230610182823013](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202306101828101.png)
$$
\begin{pmatrix}u \\ v \\ 1\end{pmatrix}=\begin{pmatrix}\alpha & 0 & t_x \\ 0 & \beta & t_y\\ 0 & 0 & 1\end{pmatrix}\begin{pmatrix}x' \\ y' \\ 1\end{pmatrix}
$$

##### 渲染采用的具体模型

![image-20230610191515981](https://cdn.jsdelivr.net/gh/SnowOnVolcano/imagebed/202306101915650.png)
$$
\begin{pmatrix}u \\ v \\ 1\end{pmatrix}=\begin{pmatrix}\alpha & 0 & t_x \\ 0 & \beta & t_y\\ 0 & 0 & 1\end{pmatrix}\begin{pmatrix}x' \\ y' \\ 1\end{pmatrix},\quad\mathbf{where}\ \ 
\begin{cases}
\alpha=image\_height/2/half\_height\\
\beta=image\_width/2/half\_width\\
t_x=image\_width/2\\
t_y=image\_height/2
\end{cases}
$$





