## Б Распределение микрограней GTR

**<font color=gray>B GTR Microfacet Distribution</font>**

### Б.1 Обзор распределения микрограней

**<font color=gray>B.1 Microfacet distribution review</font>**

Правдоподобное распределение микрограней должно быть нормализовано по полусфере таким образом, чтобы проецируемая площадь микрограней была равна 1 [^33]:

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

Значения $\gamma=3/2$ и $\gamma=2$ имеют упрощенные формы, причем последнее эквивалентно GGX:

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

Для формирования анизотропного распределения шероховатость изменяется в зависимости от $\phi$ путем замены $\frac{1}{\alpha^2}$ на $\frac{\cos^2\phi}{\alpha^2_x}+\frac{\sin^2\phi}{\alpha^2_y}$. Для $\gamma=2$ это приводит к:

<font color=gray>To form an anisotropic distribution, the roughness is varied with $\phi$ by replacing $\frac{1}{\alpha^2}$ with $\frac{\cos^2\phi}{\alpha^2_x}+\frac{\sin^2\phi}{\alpha^2_y}$. For $\gamma=2$ this results in:</font>

$$
D_{\text{GTR}_2\text{aniso}}=\frac{1}{\pi}\frac{1}{\alpha_x\alpha_y}
\frac{1}{\big(\sin^2\theta_h({\cos^2\phi_h}/{\alpha^2_x}+{\sin^2\phi_h}/{\alpha^2_y})+\cos^2\theta_h\big)^2}\qquad(10)
$$

$$
\tan\phi_h=\frac{\alpha_y}{\alpha_x}\tan(2\pi\xi_1)\qquad(11)
$$

$$
\cos\theta_h=\sqrt{\frac{1-\xi_2}{1+[1/({\cos^2\phi_h}/{\alpha^2_x}+{\sin^2\phi_h}/{\alpha^2_y})-1]\xi_2}}\qquad(12)
$$

Подстановка этих векторных тождеств

<font color=gray>Substituting these vector identities</font>

$$
\begin{array}{lcl}
    \mathbf{h}\cdot\mathbf{x}&=&\sin\theta_h\cos\phi_h\\
    \mathbf{h}\cdot\mathbf{y}&=&\sin\theta_h\sin\phi_h\\
    \mathbf{h}\cdot\mathbf{n}&=&\cos\theta_h
\end{array}
$$

в уравнение (10) дает эффективную альтернативную форму:

<font color=gray>into equation (10) produces an efficient alternate form:</font>

$$
D_{\text{GTR}_2\text{aniso}}=\frac{1}{\pi}\frac{1}{\alpha_x\alpha_y}
\frac{1}{\big((\mathbf{h}\cdot\mathbf{x})^2/{\alpha^2_x}+(\mathbf{h}\cdot\mathbf{y})^2/{\alpha^2_y}+(\mathbf{h}\cdot\mathbf{n})^2\big)^2}\qquad(13)
$$

Кроме того, разложение $\tan\phi_h$ из уравнения (11) на $\sin\phi_h$ и $\cos\phi_h$ позволяет избежать специальной обработки для квадрантов $\phi_h$, а также позволяет вычислять $\mathbf{h}$ более непосредственно:

<font color=gray>Further, factoring $\tan\phi_h$ from equation (11) into $\sin\phi_h$ and $\cos\phi_h$, avoids special handling for the quadrants of $\phi_h$ and also allows $\mathbf{h}$ to be calculated more directly:</font>

$$
\sin\phi_h=\frac{\alpha_y\sin(2\pi\xi_1)}{r}
$$

$$
\cos\phi_h=\frac{\alpha_x\cos(2\pi\xi_1)}{r}
$$

$$
\tan\theta_h=r\sqrt{\frac{\xi_2}{1-\xi_2}}
$$

$$
\mathbf{h'}=\sqrt{\frac{\xi_2}{1-\xi_2}}[{\alpha_x\cos(2\pi\xi_1)}\mathbf{x}+{\alpha_y\sin(2\pi\xi_1)}\mathbf{y}]+\mathbf{n}\qquad(14)
$$

$$
\mathbf{h}=\frac{\mathbf{h'}}{|\mathbf{h'}|}
\qquad(15)
$$

Примечание: $\mathbf{h'}$ — это *спроецированная* половина вектора, $\tan\theta_h\cos\phi_h\mathbf{x}+\tan\theta_h\sin\phi_h\mathbf{y}+\mathbf{n}$, а $r$ — это нормировочный множитель (равный $\sqrt{1/(\cos^2\phi_h/\alpha^2_x+\sin^2\phi_h/\alpha^2_y)}$), который можно игнорировать из-за сокращения.

Для произвольных значений $\gamma$ нормализация анизотропного распределения, к сожалению, не имеет замкнутой формы.

<font color=gray>Note: $\mathbf{h'}$ is the *projected* half vector, $\tan\theta_h\cos\phi_h\mathbf{x}+\tan\theta_h\sin\phi_h\mathbf{y}+\mathbf{n}$, and $r$ is a normalization factor (equal to $\sqrt{1/(\cos^2\phi_h/\alpha^2_x+\sin^2\phi_h/\alpha^2_y)}$) which can be ignored due to cancellation.

For arbitrary values of $\gamma$, the normalization of the anisotropic distribution unfortunately does not have a closed form.</font>

## Дополнение

**<font color=gray>Adenda</font>**

### Подробнее об анизотропном блеске

**<font color=gray>Anisotropic specular details</font>**

В исходных заметках опущена параметризация, которая выглядит следующим образом:

<font color=gray>The original notes omitted the parameterization which is as follows:</font>

$$ aspect=\sqrt{1-0.9anisotropic} $$

$$ \alpha_x=roughness^2/aspect $$

$$ \alpha_y=roughness^2\times{aspect} $$

Коэффициент 0.9 ограничивает соотношение сторон до 10:1.

<font color=gray>The 0.9 factor limits the aspect ratio to 10:1.</font>

### Подробности о блеске

**<font color=gray>Sheen details</font>**

В исходных заметках отсутствует описание блеска. На основе наблюдений за образцами тканей, описанных в разделе 4.5, преобладающим эффектом, отсутствующим в базовой диффузной + зеркальной модели, является дополнительная отражательная способность скольжения, наблюдаемая вдоль верхней части срезов изображения BRDF. Этот компонент очень похож на фактор Френеля. Поскольку эта форма очень похожа на френелевскую, мы моделируем ее как дополнительный лепесток BRDF, который использует форму Шлика-Френеля, $sheen\times(1-\cos\theta_d)^5$, и опционально тонируется в сторону базового цвета в соответствии с параметром $sheenTint$.

<font color=gray>The original notes omitted a description of sheen. Based on observations of the fabric samples described in section 4.5, the predominant effect missing from the base diffuse + specular model is the extra grazing reflectance seen along the top of the BRDF image slices. This component is very similar to the Fresnel factor. As this shape is very Fresnel-like, we model this as an additional BRDF lobe that uses the Schlick Fresnel shape, $sheen\times(1-\cos\theta_d)^5$, and is optionally tinted towards the base color according to the $sheenTint$ parameter.</font>

### Specular G пересмотрен

**<font color=gray>Specular G revisited</font>**

Недавно Хайц опубликовал подробный анализ функции затенения микрограней, *Understanding the Masking-Shadowing Function in Microfacet-Based BRDFs*, JCGT 2014. Хайц предложил «слабый тест белой печи» для проверки правдоподобности физически обоснованных функций маскирования и показал, что из известных функций затенения правдоподобны только модель затенения Смита [^29], [^33] и модель V-полости [^7], хотя последняя может быть менее реалистичной.
Основываясь на анализе Хайца, мы исключили наше специальное переотображение Smith $G$ для нашего первичного зеркала. Для металлов результат, очевидно, лучше, а для общих материалов это, возможно, так, особенно при рендеринге в полной среде GI с правдоподобными источниками света. Кажется весьма вероятным, что отсутствие корреляции модели Уолтера с гладкими материалами было результатом ошибки измерения в данных MERL при скользящих углах. Хайц также вывел правильную анизотропную форму затенения Смита, деталь, которую мы проигнорировали.
Для прозрачного покрытия мы по-прежнему используем изотропный лепесток GTR 1.0 с более широким хвостом и, по общему признанию, случайным фактором $G$. Это не означает, что это физически правдоподобная поверхность микрограней с соответствующим затенением и маскированием, а скорее представляет собой тонкий полупрозрачный слой, который может охватывать множественные события отражения и пропускания, и наша текущая формулировка хорошо зарекомендовала себя для большого количества материалов. Тем не менее, физическая модель, охватывающая все эти эффекты, была бы кстати.

<font color=gray>
Heitz recently published a thorough analysis of the microfacet shadowing function, *Understanding the Masking-Shadowing Function in Microfacet-Based BRDFs*, JCGT 2014. Heitz proposed the “weak white furnace test” for verifying the plausibility of physically based masking functions and showed that, of known shadowing functions, only the Smith shadowing model [29], [33] and the V-cavity model [7] are plausible, though the latter may be less realistic.
Based on Heitz’ analysis, we have eliminated our ad-hoc remapping of Smith $G$ for our primary specular. For metals, the result is obviously better, and for general materials it is arguably so, especially when rendering in a full GI environment with plausible light sources. It seems very likely that the lack of correlation of the Walter model to the smooth materials was a result of measurement error in the MERL data at grazing angles. Heitz also derived the correct anisotropic form of the Smith shadowing, a detail we had neglected.
For clearcoat, we still use the isotropic GTR 1.0 lobe with the wider tail and the admittedly ad-hoc $G$ factor. This is not meant to represent a physically plausible microfacet surface with corresponding shadowing and masking, but rather it is representing a thin, translucent layer that may encompass multiple reflection and transmission events, and our current formulation has worked well for a large variety of materials. That said, a physical model that encompassed all of these effects would be welcome.</font>

### История изменений

    Версия 2 (31 августа 2012 г.): исправлен коэффициент нормализации в уравнении 4.
    Версия 3 (12 августа 2014 г.): исправлено форматирование для уравнений 10–13; добавлены дополнения.
