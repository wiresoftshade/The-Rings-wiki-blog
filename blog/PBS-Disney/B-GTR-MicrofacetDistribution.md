## Б Распределение микрограней GTR

**<font color=gray>B GTR Microfacet Distribution</font>**

### Б.1 Обзор распределения микрограней

**<font color=gray>B.1 Microfacet distribution review</font>**

Правдоподобное распределение микрограней должно быть нормализовано по полусфере таким образом, чтобы проецируемая площадь микрограней была равна 1 [33]:

<font color=gray>A plausible microfacet distribution must be normalized over the hemisphere such that the projected area of the microfacets is 1 [33]:</font>

$$
\int_{\Omega}D(\theta_h)\cos\theta_hd\omega=1
$$

или в сферических координатах:

<font color=gray>or in spherical coordinates:</font>

$$
\int^{2\pi}_0\int^{\pi/2}_0D(\theta_h)\cos\theta_h\sin\theta_hd\theta_hd\phi_h=1
$$

<!-- \mathrm{d} -->

Для выборки по важности удобно выбрать $pdf_h=D(\theta_h)\cosθ_h$, учитывая, что она уже нормализована. Обратите внимание, $pdf_h$ — это плотность относительно половины вектора; плотность относительно вектора света $\boldsymbol{l}$ равна:

<font color=gray>For importance sampling, it is convenient to choose $pdf_h=D(\theta_h)\cosθ_h$ given that it is already normalized. Note, $pdf_h$ is the density with respect to the half vector; the density with respect to the light vector $\boldsymbol{l}$ is:</font>

$$
pdf_l=\frac{pdf_h}{4(\boldsymbol{l}\cdot\boldsymbol{h})}
$$

Для генерации выборок по полусфере pdf разбивается на сферические компоненты, $pdf_h=pdf_{\theta_h}pdf_{\phi_h}$. Для изотропных распределений эта факторизация тривиальна, поскольку распределение не зависит от $\phi_h$ и $pdf_{\phi_h}=\frac{1}{2\pi}$. Для анизотропных распределений факторизация выполняется путем интегрирования из $\theta_h$ для получения:

<font color=gray>To generate samples over the hemisphere, the pdf is split into spherical components, $pdf_h=pdf_{\theta_h}pdf_{\phi_h}$. For isotropic distributions this factorization is trivial as the distribution has no dependence on $\phi_h$ and $pdf_{\phi_h}=\frac{1}{2\pi}$. For anisotropic distributions, the factorization is accomplished by integrating out $\theta_h$ to get:</font>

$$
pdf_{\phi_h}=\int^{\frac\pi2}_0pdf_hd\theta_h
$$

$$
pdf_{\theta_h}=\frac{pdf_h}{pdf_{\phi_h}}
$$

Затем каждый компонент pdf интегрируется для формирования cdf, а затем инвертируется для формирования соответствующей функции выборки:

<font color=gray>Each component pdf is then integrated to form a cdf and then inverted to form a corresponding
sampling function:</font>

$$
cdf(x)=\int^x_0pdf_xdx
$$

$$
x=cdf^{-1}(\xi)
$$

Учитывая две функции выборки и равномерные случайные величины $\xi_1$ и $\xi_2$, $\theta_h$ и $\phi_h$ можно вычислить и спроецировать в систему координат вокруг нормали $\mathbf{n}$, касательной $\mathbf{x}$ и бикасательной $\mathbf{y}$ для формирования половины вектора $\mathbf{h}$. Наконец, если задан вектор $\mathbf{v}$, $\mathbf{l}$ можно вычислить, отразив $\mathbf{h}$ относительно $\mathbf{v}$: 

<font color=gray>Given the two sampling functions and uniform random variables $\xi_1$ and $\xi_2$, $\theta_h$ and $\phi_h$ can be computed and projected to the coordinate frame around the normal $\mathbf{n}$, tangent $\mathbf{x}$, and bitangent $\mathbf{y}$ to form the half vector $\mathbf{h}$. Finally, given a $\mathbf{v}$ vector, $\mathbf{l}$ can be computed by reflecting $\mathbf{h}$ across $\mathbf{v}$:</font>

$$
\mathbf{h}=\sin\theta_h\cos\phi_h\mathbf{x}+\sin\theta_h\sin\phi_h\mathbf{y}+\cos\theta_h\mathbf{n}
$$

$$
\mathbf{l}=2(\mathbf{v}\cdot\mathbf{h})\mathbf{h}−\mathbf{v}
$$

### Б.2 GTR
**<font color=gray>B.2 GTR</font>**

После приведенных выше выводов нормализованные уравнения распределения GTR и выборки имеют вид:

<font color=gray>Following the above derivations, the normalized GTR distribution and sampling equations are:</font>

$$
D_\text{GTR}(\theta_h)=\frac{(\gamma-1)(\alpha^2-1)}{\pi(1-(\alpha^2)^{1-\gamma})}\frac{1}{(1+(\alpha^2-1)\cos^2\theta_h)^\gamma}\qquad(1)
$$

$$
\phi_h=2\pi\xi_1\qquad(2)
$$

$$ 
\cos\theta_h=\sqrt{\frac{1-[(\alpha^2)^{1-\gamma}(1-\xi_2)+\xi_2]^{\frac{1}{1-\gamma}}}{1-\alpha^2}}\qquad(3)
$$

Это распределение справедливо для любого $\gamma>0$, однако при $\gamma=1$ возникает сингулярность. Принимая предел как $\gamma\longrightarrow1$, получаем эту альтернативную форму:

<font color=gray>This distribution is valid for any $\gamma>0$, however, at $\gamma=1$ there is a singularity. Taking the limit as $\gamma\longrightarrow1$ produces this alternate form:</font>

$$
D_{\text{GTR}_1}(\theta_h)=\frac{\alpha^2-1}{\pi\log\alpha^2}\frac{1}{(1+(\alpha^2-1)\cos^2\theta_h)}\qquad(4)
$$

$$
\cos\theta_h=\sqrt{\frac{1-(\alpha^2)^{1-\xi_2}}{1-\alpha^2}}\qquad(5)
$$

Значения $\gamma=3/2$ и $\gamma=2$ имеют упрощенные формы, причем последнее эквивалентно GTX:

<font color=gray>The values of $\gamma=3/2$ and $\gamma=2$ have simplified forms, the latter being equivalent to GGX:</font>


$$
D_{\text{GTR}_{3/2}}(\theta_h)=\frac{\alpha^2+\alpha}{2\pi}\frac{1}{(1+(\alpha^2-1)\cos^2\theta_h)^{3/2}}\qquad(6)
$$

$$
\cos\theta_h=\sqrt{\frac{1}{1-\alpha^2}\bigg(1-\frac{\alpha^2}{(1+(\alpha-1)\xi_2)^2}\bigg)}\qquad(7)
$$

$$
D_{\text{GTR}_2}(\theta_h)=\frac{\alpha^2}{\pi}\frac{1}{(1+(\alpha^2-1)\cos^2\theta_h)^2}\qquad(8)
$$

$$
\cos\theta_h=\sqrt{\frac{1-\xi_2}{1+(\alpha^2-1)\xi_2}}\qquad(9)
$$