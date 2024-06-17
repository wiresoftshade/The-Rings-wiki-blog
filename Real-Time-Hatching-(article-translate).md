# Real-Time Hatching

Emil Praun Hugues Hoppe Matthew Webb Adam Finkelstein

Princeton University Microsoft Research Princeton University Princeton University

## Abstract

Drawing surfaces using hatching strokes simultaneously conveys material, tone, and form. We present a real-time system for nonphotorealistic rendering of hatching strokes over arbitrary surfaces. During an automatic preprocess, we construct a sequence of mipmapped hatch images corresponding to different tones, collectively called a _tonal art map_. Strokes within the hatch images are scaled to attain appropriate stroke size and density at all resolutions, and are organized to maintain coherence across scales and tones. At runtime, hardware multitexturing blends the hatch images over the rendered faces to locally vary tone while maintaining both spatial and temporal coherence. To render strokes over arbitrary surfaces, we build a lapped texture parametrization where the overlapping patches align to a curvature-based direction field. We demonstrate hatching strokes over complex surfaces in a variety of styles.

## Абстракция

Рисование поверхностей штриховкой одновременно передает материал, тон и форму. Мы представляем систему реального времени для нефотореалистичного рендеринга штрихов на произвольных поверхностях. Во время автоматической предварительной обработки мы создаем последовательность штрих-изображений с мип-отображением, соответствующих различным тонам, которые вместе называются _тональными художественными картами_. Штрихи в изображениях штриховки масштабируются для достижения соответствующего размера и плотности штрихов при всех разрешениях и организованы для обеспечения согласованности масштабов и тонов. Во время выполнения аппаратное мультитекстурирование смешивает изображения штриховки с визуализированными лицами для локального изменения тона, сохраняя при этом как пространственную, так и временную согласованность. Для рендеринга штрихов на произвольных поверхностях мы создаем параметризацию перекрывающейся текстуры, в которой перекрывающиеся участки выравниваются по полю направления на основе кривизны. Мы демонстрируем штриховки на сложных поверхностях в различных стилях.

**Keywords:** non-photorealistic rendering, line art, multitexturing, chicken-and-egg problem

...

## 4 Automatic generation of line-art TAMs

## 4 Автоматическая генерация художественности штрихов ТАМов

The concept of tonal art maps is quite general and can be used to represent a variety of aesthetics (e.g. pencil, crayon, stippling, and charcoal). The grid of images in the TAM can be either hand-drawn or generated automatically. In this section we present our technique for automatically generating a line-art TAM. 

Концепция тональных карт довольно общая и может использоваться для представления различных эстетик (например, карандаша, мелка, штриховки и угля). Сетка изображений в ТАМ может быть нарисована вручную или сгенерирована автоматически. В этом разделе мы представляем нашу технику автоматического создания линейного ТАМ.

Recall that the strokes in the resulting TAM should satisfy the nesting property described in the previous section. Our approach is to fill the TAM images in top-to-bottom, left-to-right order. For each column, we begin by copying all the images from the column to its left (or setting all images to white when starting at the leftmost column). This ensures that all strokes in images with lighter tone also appear in images with darker tone. Within the column, we then consider each image in top-to-bottom (coarse-to-fine) order. We repeatedly add strokes to the image until the mean image tone reaches the tone value associated with that column. Each stroke drawn in the image is also added to all the lower (finer) images in the current column. This ensures that strokes in coarser images always appear in finer images.

Напомним, что штрихи в полученном TAM должны удовлетворять свойству вложенности, описанному в предыдущем разделе. Наш подход заключается в заполнении изображений TAM сверху вниз и слева направо. Для каждого столбца мы начинаем с копирования всех изображений из столбца слева от него (или делаем все изображения белыми, начиная с крайнего левого столбца). Это гарантирует, что все штрихи на изображениях более светлых тонов также будут отображаться на изображениях более темных тонов. Затем внутри столбца мы рассматриваем каждое изображение в порядке сверху вниз (от грубого к мелкому). Мы неоднократно добавляем штрихи к изображению, пока средний тон изображения не достигнет значения тона, связанного с этим столбцом. Каждый штрих, нарисованный на изображении, также добавляется ко всем нижним (более мелким) изображениям в текущем столбце. Это гарантирует, что штрихи на более грубых изображениях всегда будут отображаться на более мелких изображениях.

The naive approach of random stroke selection leads to a non-uniform distribution of strokes, as illustrated in the figure to the right. Typically an artist would space the strokes more evenly. To get even spacing, we generate multiple randomly-placed candidate strokes and select the “best-fitting” one. In the case of the TAM shown in Figure 2, the number of candidates is set to 1000 for the light-tone images where spacing is important, and is gradually reduced to 100 for the darktone images where strokes overlap. The length of each candidate stroke is randomly set to between 0.3 and 1.0 times the width of the image, and its orientation has a tiny random perturbation from the mean. Other TAMs shown in Figure 5 use different parameters. 

Наивный подход к выбору случайных штрихов приводит к неравномерному распределению штрихов, как показано на рисунке справа. Обычно художник размещает мазки более равномерно. Чтобы добиться равномерного интервала, мы генерируем несколько случайно расположенных возможных штрихов и выбираем «наиболее подходящий». В случае ТАМ, показанного на Рисунке 2, количество кандидатов установлено равным 1000 для изображений светлых тонов, где интервал важен, и постепенно уменьшается до 100 для изображений темных тонов, где штрихи перекрываются. Длина каждого кандидатного штриха случайным образом устанавливается в диапазоне от 0,3 до 1,0 ширины изображения, а его ориентация имеет небольшое случайное отклонение от среднего значения. Другие ТАМ, показанные на Рисунке 5, используют другие параметры.

_Figure 2: A Tonal Art Map. Strokes in one image appear in all the images to the right and down from it._

_Figure 5: Results. Six models rendered with different TAMs, indicated in the inset texture patches._

Our measure of “best-fitting” includes both progress towards the desired tone value and hatching uniformity. For each candidate stroke $s_i$ we measure its progress as follows. For the hatch image at each level $l$ of the TAM that would receive $s_i$, we find the average tones, $T_l$ and $T^i_l$ , respectively, of the hatch image drawn with all previously chosen strokes and with $s_i$ added. The sum ${\sum} _l(T^i_l-T_l)$ expresses the darkness that this stroke would add to all the hatch images in this column – essentially a measure of the progress toward the desired tone at all levels of the TAM.
 
Наша мера «наилучшего соответствия» включает в себя как прогресс в достижении желаемого значения тона, так и однородность штриховки. Для каждого кандидатного штриха $s_i$ мы измеряем его прогресс следующим образом. Для изображения штриховки на каждом уровне $l$ ТАМ, которое получит $s_i$, мы находим средние тона $T_l$ и $T^i_l$ соответственно для изображения штриховки, нарисованной со всеми ранее выбранными штрихами и с добавлением $s_i$. Сумма ${\sum}_l(T^i_{l}-T_{l})$ выражает темноту, которую этот штрих добавит ко всем изображениям штриховки в этом столбце – по сути, это мера продвижения к желаемому тону на всех уровнях ТАМ.

_Figure 3: Rendering using tonal art maps. (a) illustrates resolution changes using custom mipmaps; (b) shows smooth changes in tone and (c) shows their interplay on a shaded sphere._ 

To achieve greater hatching uniformity, we maintain an image pyramid for each unfilled image in the TAM column, and find the cumulative effect of adding $s_i$ at all levels $p$ of these pyramids. Even though $s_i$ might lie next to, but not overlap, an existing stroke at fine levels of a pyramid, it will overlap at coarser levels. Thus we find the average tones ${T_{pl}}$ and ${T^i_{pl}}$ (without and with $s_i$ , respectively) over each level $p$ of every pyramid, and sum $\sum_{p,l}(T^i_{pl}-T_{pl})$. 

Чтобы добиться большей однородности штриховки, мы сохраняем пирамиду изображений для каждого незаполненного изображения в столбце TAM и находим совокупный эффект от добавления $s_i$ на всех уровнях $p$ этих пирамид. Даже если $s_i$ может лежать рядом с существующей чертой на мелких уровнях пирамиды, но не перекрывать ее, она будет перекрываться на более грубых уровнях. Таким образом, мы находим средние тона ${T_{pl}}$ и ${T^i_{pl}}$ (без и с $s_i$ соответственно) по каждому уровню $p$ каждой пирамиды и суммируем ${\sum} _{p,l}(T^i_{pl}-T_{pl})$.

Finally, this simultaneous measure of progress and hatching uniformity favors longer strokes over shorter strokes, even at the expense of overlapping a previous stroke. Therefore, we normalize the “goodness” of the stroke by its length, measuring the goodness of $s_i$ as: $\frac{1}{||s_i||}$ ${\sum} _{p,l}(T^i_{pl}-T_{pl})$. With optimized stroke placement, the hatch images are much more uniform, as illustrated in Figures 2.

Наконец, этот одновременный показатель прогресса и однородности штриховки отдает предпочтение более длинным штрихам по сравнению с более короткими, даже за счет перекрытия предыдущего штриха. Поэтому мы нормализуем «качественность» штриха по его длине, измеряя качество $s_i$ как: $\frac{1}{||s_i||}$ ${\sum} _{p,l}(T^i_{pl}-T_{pl})$. Благодаря оптимизированному расположению штрихов изображения штриховки становятся гораздо более однородными, как показано на Рисунках 2.

Artists often use parallel strokes to represent lighter tones, and switch to cross-hatching for darker tones. Our TAM construction process supports cross-hatching, as demonstrated in Figure 2. For some number of leftmost columns (e.g. 3), we add only horizontal strokes. Then, beginning with some middle column (e.g. 4th), we add only vertical strokes for cross-hatching. Finally, some number of columns later (e.g. 6th), we add _both_ vertical and horizontal strokes to best fill the remaining gaps. 

Художники часто используют параллельные штрихи для изображения более светлых тонов и переходят на перекрестную штриховку для более темных тонов. Наш процесс построения TAM поддерживает перекрестную штриховку, как показано на рисунке 2. Для некоторого количества крайних левых столбцов (например, 3-го) мы добавляем только горизонтальные штрихи. Затем, начиная с какого-нибудь среднего столбца (например, 4-го), добавляем только вертикальные штрихи для перекрестной штриховки. Наконец, через некоторое количество столбцов (например, 6-го) мы добавляем _оба_. Как вертикальные, так и горизонтальные штрихи, чтобы лучше заполнить оставшиеся пробелы.

In our current implementation, stylistic variation (Figure 5) between different TAMs comes from the variation in angle, crosshatching schedule, range of lengths, and choice of stroke (given as a grayscale image). For now we only use grayscale strokes, to enable an efficient rendering scheme described in the next section. The finest hatch images are 256×256, and are toroidal to allow for tiled rendering over parametrized surfaces.

В нашей текущей реализации стилистические вариации (Рис. 5) между различными TAM происходят из-за различий в угле, графике штриховки, диапазоне длин и выборе штриха (представленного в виде изображения в оттенках серого). На данный момент мы используем только штрихи в оттенках серого, чтобы обеспечить эффективную схему рендеринга, описанную в следующем разделе. Самые мелкие изображения штриховки имеют размер 256×256 и имеют тороидальную форму, что позволяет выполнять мозаичный рендеринг на параметризованных поверхностях.


## 5 Rendering with TAMs

## 5 Визуальзация с ТАМ-ами

The nesting structure in the TAM image grid helps to provide temporal coherence during animation. The mip-mapping feature of hardware texturing automatically blends between different resolution levels of the TAM. What is missing, however, is a smooth transition in the tonal dimension of the TAM. We achieve smooth transitions using a 6-way blending scheme that we will describe shortly. However, we first present three intermediate approximations. 

Структура вложенности в сетке изображения TAM помогает обеспечить временную согласованность во время анимации. Функция мип-мэппинга аппаратного текстурирования автоматически смешивает различные уровни разрешения TAM. Однако чего не хватает, так это плавного перехода тонального измерения ТАМ. Мы добиваемся плавных переходов, используя 6-ступенчатую схему смешивания, которую мы вскоре опишем. Однако сначала мы представим три промежуточных приближения.

First, if for each face we select a single tone column from the TAM (equivalent to flat shading with a quantized palette), our rendering suffers from both spatial discontinuities across edges (see adjacent figure) and temporal discontinuities (“pops” in tone). Second, the analog of conventional flat shading is to interpolate between two consecutive tone columns using a single blend ratio for all pixels in a face. This effect is temporally smooth, but looks faceted. For spatial coherence we need to blend vertex contributions across each face. Thus, our third scheme selects a single tone column per vertex and blends tones across faces. This scheme is spatially smooth but suffers from temporal discontinuities due to tonal value rounding. (This third scheme is equivalent to Gouraud-shading with severely quantized vertex lighting computations.) 

Во-первых, если для каждой грани мы выбираем один столбец тона из TAM (эквивалент плоского затенения с квантованной палитрой), наш рендеринг страдает как от пространственных разрывов по краям (см. соседний рисунок), так и от временных разрывов («всплески» в тонах). Во-вторых, аналогом обычного плоского затенения является интерполяция между двумя последовательными столбцами тонов с использованием единого коэффициента смешивания для всех пикселей лица. Этот эффект временно сглажен, но выглядит граненым. Для пространственной когерентности нам необходимо смешать вклады вершин на каждой грани. Таким образом, наша третья схема выбирает один столбец тонов для каждой вершины и смешивает тона на гранях. Эта схема пространственно гладкая, но страдает от временных разрывов из-за округления тональных значений. (Эта третья схема эквивалентна затенению по Гуро со строго квантованными вычислениями вершинного освещения.)

To obtain both spatial and temporal coherence, we bracket the continuous tone at each mesh vertex (blending between two consecutive tone images). Then, for each mesh face, we gather the blended textures at the three vertices and spatially combine them across the face (using a barycentric sum as in Gouraud shading). Since both the 2-way tonal blend and 3-way spatial blend are linear combinations, this amounts to linearly blending 6 images across the face (or 12 images when taking into account mip-mapping). The process is illustrated in Figure 4. While this complex blend operation may initially appear daunting, there are several ways of implementing it efficiently on commodity graphics hardware. We next present two such schemes.

Чтобы получить как пространственную, так и временную когерентность, мы заключаем непрерывный тон в каждую вершину сетки (смешивание двух последовательных тональных изображений). Затем для каждой грани сетки мы собираем смешанные текстуры в трех вершинах и пространственно объединяем их по грани (используя барицентрическую сумму, как при затенении Гуро). Поскольку и двухстороннее тональное смешение, и трехстороннее пространственное смешение представляют собой линейные комбинации, это равносильно линейному смешиванию 6 изображений по лицу (или 12 изображений с учетом мип-маппинга). Этот процесс показан на Рисунке 4. Хотя эта сложная операция смешивания может поначалу показаться сложной, существует несколько способов эффективной реализации ее на обычном графическом оборудовании. Далее мы представим две такие схемы.
 
**Single-pass 6-way blend.** The 6-way blend can be implemented in a single rendering pass. Several existing graphics card support 2 texture reads during rasterization (and that number will soon jump to 4). Exploiting the fact that our TAM images are grayscale, we pack 6 consecutive tone images in the R,G,B channels of two texture images. The diffuse and specular fragment colors encode the blend ratios. We set these color values at vertices, and the hardware interpolates them at pixel locations. The 6 tones are combined by adding two dot products between the texture colors and the fragment colors. The first multitexture stage performs the two dot products, while the second stage adds the results. 

Hertzmann and Zorin [7] observe that effective drawings can use a limited palette of tones, and their scheme targets 4 tone levels. For our examples, we chose to define 6 tone levels, so that the TAM images can be packed in two textures used over all triangles. Since the texture state remains constant, we use triangle strips for efficiency. We store vertex geometry and texture coordinates on the graphics card in vertex arrays, whereas the diffuse and specular vertex colors must be copied from main memory for every frame. With newly-emerging graphics cards, however, these could also be computed on the GPU using vertex shaders. 

Our set of 6 tones do not include white – the “paper” color. However, our interpolation method provides for an implicit white as follows. Since the coefficients of a convex combination sum to 1.0, by specifying 6 independent coefficients we can implicitly blend 7 tones – the 7th tone being 0.0 (black). Since we prefer white, we negate the texture inputs before the dot products, as well as the resulting sum. Thus, the images in our paper are rendered using 6-column TAMs (containing strokes) as well as implicit white. 
When hatching surfaces of arbitrary topology using lapped textures, rendering is complicated by the need to modulate each patch texture by the patch outline alpha mask. We address this problem in Section 6. 

**Однопроходное 6-ходовое смешивание.** Шестиэтапное смешение может быть реализовано за один проход рендеринга. Некоторые существующие видеокарты поддерживают 2 чтения текстур во время растеризации (и это число скоро увеличится до 4). Используя тот факт, что наши изображения TAM имеют оттенки серого, мы упаковываем 6 последовательных тоновых изображений в каналы R, G, B двух изображений текстур. Цвета диффузных и зеркальных фрагментов кодируют пропорции смешивания. Мы устанавливаем эти значения цвета в вершинах, а оборудование интерполирует их в точках пикселей. 6 тонов объединяются путем добавления двух скалярных произведений между цветами текстуры и цветами фрагментов. На первом этапе мультитекстуры выполняются два скалярных произведения, а на втором этапе результаты суммируются. 

Hertzmann и Zorin [7] отмечают, что в эффективных рисунках можно использовать ограниченную палитру тонов, а их схема рассчитана на 4 уровня тонов. Для наших примеров мы решили определить 6 уровней тона, чтобы изображения TAM можно было упаковать в две текстуры, используемые для всех треугольников. Поскольку состояние текстуры остается постоянным, для эффективности мы используем треугольные полоски. Мы храним геометрию вершин и координаты текстур на видеокарте в массивах вершин, тогда как диффузные и зеркальные цвета вершин должны копироваться из основной памяти для каждого кадра. Однако с появлением новых видеокарт их можно также вычислять на GPU с использованием вершинных шейдеров. 

В нашем наборе из 6 тонов нет белого – «бумажного» цвета. Однако наш метод интерполяции предусматривает неявный белый цвет следующим образом. Поскольку сумма коэффициентов выпуклой комбинации равна 1.0, задав 6 независимых коэффициентов, мы можем неявно смешать 7 тонов, причем 7-й тон равен 0.0 (черный). Поскольку мы предпочитаем белый цвет, мы инвертируем входные данные текстуры перед скалярным произведением, а также результирующую сумму. Таким образом, изображения в нашей статье визуализируются с использованием 6-колоночных TAM (содержащих штрихи), а также неявного белого цвета. 
При штриховке поверхностей произвольной топологии с использованием перекрывающихся текстур рендеринг усложняется необходимостью модулировать каждую текстуру патча с помощью альфа-маски контура патча. Эту проблему мы рассмотрим в разделе 6.

**Triple-pass 2-way blend.** If the TAM images contain colored strokes, or if the artist desires more than 6 TAM tone images, an alternative scheme is to accumulate texture over each face in 3 passes. The scheme begins by drawing the whole mesh in black. Next  it renders each triangle 3 times, adding the contribution of each vertex to the framebuffer. For each vertex we interpolate between the two TAM columns that bracket the vertex tone. A simple optimization is to organize the faces in triangle fans around each vertex.

**Трехпроходное 2-ходовое смешивание.** Если изображения ТАМ содержат цветные штрихи или если художник желает использовать более 6 изображений тонов ТАМ, альтернативной схемой является накопление текстуры на каждом лице за 3 прохода. Схема начинается с рисования всей сетки черным цветом. Затем он визуализирует каждый треугольник 3 раза, добавляя вклад каждой вершины в буфер кадра. Для каждой вершины мы интерполируем между двумя столбцами TAM, которые заключают в себе тон вершины. Простая оптимизация — организовать грани в виде вееров треугольников вокруг каждой вершины.

_(a) (b) (c) (d) Figure 4: Illustration of the blending of 6 TAM images on a triangle face. Each column (a–c) corresponds to a vertex and shows the images for the floor and ceiling of the vertex tone. The resulting sum is shown in (d)._ 

**Tone thresholding.** The 6-way blend scheme obtains coherence, but results in the appearance of some gray-toned strokes. Such strokes look natural for a variety of artistic styles including pencil and charcoal, but are not ideal for some ink-based strokes. To more closely match ink strokes, we have experimented with thresholding the tone values written to the framebuffer. For the single-pass blending scheme, we can configure the multitexturing register combiners to obtain the transfer function clamp(8t − 3.5), which closely models a step function. This transfer function succeeds in making new strokes appear as gradually lengthening black strokes instead of gradually darkening gray strokes. Unfortunately, as shown on the accompanying video, it has the side-effect of introducing jaggies along the carefully antialiased edges of the visible strokes. It may be possible to alleviate these artifacts through framebuffer supersampling.

**Установление порога тона.** Схема 6-ходного наложения обеспечивает согласованность, но приводит к появлению некоторых серых штрихов. Такие мазки выглядят естественно для различных художественных стилей, включая карандаш и уголь, но не идеальны для некоторых мазков на основе чернил. Чтобы более точно соответствовать рукописным штрихам, мы экспериментировали с пороговым значением значений тона, записываемых в буфер кадра. Для схемы однопроходного смешивания мы можем настроить объединители регистров мультитекстурирования для получения передаточной функции (8t − 3.5), которая точно моделирует ступенчатую функцию. Благодаря этой передаточной функции новые штрихи выглядят как постепенно удлиняющиеся черные штрихи, а не как постепенно затемняющиеся серые штрихи. К сожалению, как показано в сопроводительном видео, это имеет побочный эффект: неровности вдоль тщательно сглаженных краев видимых штрихов. Эти артефакты можно устранить с помощью суперсэмплинга кадрового буфера. (Или при использовании полей дистанций. Прим. ред.)

## 6 Applying TAMs to arbitrary surfaces

## 6 Применение ТАМ к произвольным поверхностям

For parametrized surfaces, one can apply the TAM rendering algorithm described in Section 5 directly. For example, the sphere and cylinder shown in Figure 3 were textured using a simple tiling of a toroidal TAM. However, for surfaces that lack natural global parametrizations, or for which this parametrization is too distorted, we use lapped textures.

Для параметризованных поверхностей можно напрямую применить алгоритм рендеринга TAM, описанный в разделе 5. Например, сфера и цилиндр, показанные на рисунке 3, были текстурированы с использованием простой мозаики тороидального ТАМ. Однако для поверхностей, у которых отсутствует естественная глобальная параметризация или для которых эта параметризация слишком искажена, мы используем текстуры с перекрытием.

To review, lapped textures were introduced by Praun et al. [17] as a way to texture surfaces of arbitrary topology without the need for a continuous global parametrization. The key observation is that the surface can be covered by a collection of overlapping patches. All the patches are constructed as topological discs, and are parameterized over the plane with little distortion. For many textures, including our TAMs, the boundaries between the patches are not noticeable, being masked by the high frequency detail of the textures. Visual masking is further helped by constructing the patches with irregularly shaped boundaries and with small alpha ramps that “feather” the boundaries.

Для обзора Praun и др. [17] представили перекрытые текстуры как способ текстурирования поверхностей произвольной топологии без необходимости непрерывной глобальной параметризации. Ключевое наблюдение заключается в том, что поверхность может быть покрыта набором перекрывающихся участков. Все патчи построены в виде топологических дисков и параметризованы по плоскости с небольшими искажениями. Для многих текстур, в том числе и для наших ТАМ, границы между патчами не заметны, маскируясь высокочастотной детализацией текстур. Визуальной маскировке также способствует создание участков с границами неправильной формы и небольшими альфа-рампами, которые «растушёвывают» границы.

Hatch images are ideal for use with lapped textures, because they lack lowfrequency components (which otherwise might reveal the patch boundaries). To render a surface as a lapped texture using TAMs, we apply the algorithm is Section 5 for each of the patches, shown in random tone to the right. We modify the original lapped texture rendering algorithm to adapt it for hatch rendering by decoupling the patch outline from the stroke textures, storing them separately. When rendering a patch, we first render its triangles textured using the patch outline mask, in order to store this mask into the alpha channel of the framebuffer. Next, when rendering the patch triangles using the TAM texture images, the blend operation is set to add the pixels being rendered, multiplied by the alpha value already present in the  framebuffer. (During this operation, only the color channels of the framebuffer are written.) As an alternative useful for rendering into visuals that do not have an alpha channel, the modulation by the patch outline may be done using a texture unit. To implement this on graphics cards that allow only two texture reads per pixel, the consecutive tonal levels to be averaged have to be packed inside a single texture (see Section 5).

Штриховые изображения идеально подходят для использования с перекрывающимися текстурами, поскольку в них отсутствуют низкочастотные компоненты (которые в противном случае могли бы выявить границы участков). Чтобы визуализировать поверхность в виде наложенной текстуры с использованием TAM, мы применяем алгоритм, описанный в разделе 5, для каждого из патчей, показанных случайным тоном справа. Мы модифицируем исходный алгоритм рендеринга перекрывающихся текстур, чтобы адаптировать его для рендеринга штриховки, отделяя контур патча от текстур обводки и сохраняя их отдельно. При рендеринге патча мы сначала визуализируем его треугольники, текстурированные с использованием маски контура патча, чтобы сохранить эту маску в альфа-канале фреймбуфера. Далее, при рендеринге треугольников патчей с использованием изображений текстуры TAM, операция смешивания устанавливается для сложения визуализируемых пикселей, умноженных на значение альфа, уже присутствующее в буфере кадра. (Во время этой операции записываются только цветовые каналы кадрового буфера.) В качестве альтернативы, полезной для рендеринга в визуальные эффекты, не имеющие альфа-канала, модуляция контуром патча может выполняться с использованием текстурного модуля. Чтобы реализовать это на видеокартах, которые допускают только два чтения текстур на пиксель, последовательные усредняемые уровни тонов должны быть упакованы в одну текстуру (см. раздел 5).

Decoupling the patch shape from the hatch textures presents several advantages. First, it reduces memory consumption, since we only have to store the outline once, and not replicate it for every image in the TAM. Second, having a separate texture transform for the hatch texture allows us to rotate and scale the strokes within a patch at runtime, without the need to recompute the lapped parametrization. Third, the stroke textures can be tiled in order to cover large patches. Finally, as a consequence of having a different scale for the outline than for the strokes, we can place different size patches on differents parts of the surface (smaller patcher in areas with high curvature, larger patches in flat regions), achieving better coverage while using just a single patch outline. In the original lapped textures work, having different size patches could only be achieved using multiple outlines.

Отделение формы пятна от текстур штриховки дает несколько преимуществ. Во-первых, это снижает потребление памяти, поскольку нам нужно сохранить контур только один раз, а не дублировать его для каждого изображения в TAM. Во-вторых, наличие отдельного преобразования текстуры для текстуры штриховки позволяет нам вращать и масштабировать штрихи внутри патча во время выполнения без необходимости пересчитывать перекрывающуюся параметризацию. В-третьих, текстуры обводок можно располагать в виде мозаики, чтобы покрыть большие участки. Наконец, благодаря тому, что у контура разный масштаб, чем у штрихов, мы можем размещать патчи разного размера на разных частях поверхности (меньший патчер в областях с высокой кривизной, большие патчи в плоских областях), достигая лучшего покрытия и одновременно используя только один контур патча. В исходной работе с наложенными текстурами наличие участков разного размера можно было добиться только с помощью нескольких контуров.

Anisotropic lapped textures need a direction field for the parametrization. In our project, the field governs the direction of strokes on the surface. Girshick et al. [3] observed that stroke direction augments the viewer’s perception of shape, and that principal curvatures are a natural choice for direction. Hertzmann and Zorin [7] point out that in many drawings the hatch direction follows the curvature of the overall shape, whereas fine details are expressed through tonal variation. Consequently, we compute curvatures on the faces of a simplified version of the mesh, smooth the resulting direction field, and then resample it on the original mesh. For every face of the coarse mesh, we gather the set of vertices adjacent to any of the face’s vertices. We then fit a quadric through these vertices, and finally compute principal curvature directions for this quadric. The error residual from the fit, as well as the ratio of the curvatures, provides a measure of confidence for the computed directions. Now that we have defined these directions for every face, we smooth the field, blending directions from high-confidence areas into low-confidence areas. We use a global non-linear optimization similar to the one described by Hertzmann and Zorin [7], but adapted for 180◦ rather than 90◦ symmetries.

Для параметризации анизотропных перекрывающихся текстур требуется поле направлений. В нашем проекте поле определяет направление штрихов на поверхности. Girshick и др. [3] заметили, что направление штриха улучшает восприятие формы зрителем и что основные кривизны являются естественным выбором направления. Hertzmann и Zorin [7] отмечают, что на многих рисунках направление штриховки повторяет кривизну общей формы, тогда как мелкие детали выражаются посредством тональных вариаций. Следовательно, мы вычисляем кривизну на гранях упрощенной версии сетки, сглаживаем полученное поле направлений, а затем повторно дискретизируем его на исходной сетке. Для каждой грани грубой сетки мы собираем набор вершин, смежных с любой из вершин грани. Затем мы проходим через эти вершины квадрику и, наконец, вычисляем главные направления кривизны этой квадрики. Остаточная ошибка аппроксимации, а также соотношение кривизн обеспечивают меру достоверности вычисленных направлений. Теперь, когда мы определили эти направления для каждого лица, мы сглаживаем поле, смешивая направления из областей с высокой достоверностью в области с низкой достоверностью. Мы используем глобальную нелинейную оптимизацию, аналогичную описанной Hertzmann и Zorin [7], но адаптированную для симметрии 180◦, а не 90◦.

...

## References

[1] Deussen, O., and Strothotte, T. Computer-Generated Pen-and-Ink Illustration of
Trees. Proceedings of SIGGRAPH 2000, 13–18.

[2] Elber, G. Interactive Line Art Rendering of Freeform Surfaces. Computer
Graphics Forum 18, 3 (September 1999), 1–12.

[3] Girshick, A., Interrante, V., Haker, S., and Lemoine, T. Line Direction
Matters: An Argument for the Use of Principal Directions in 3D Line Drawings.
Proceedings of NPAR 2000, 43–52.

[4] Gooch, B., Sloan, P.-P. J., Gooch, A., Shirley, P., and Riesenfeld, R. Interactive
Technical Illustration. 1999 ACM Symposium on Interactive 3D Graphics, 31–
38.

[5] Haeberli, P. E. Paint By Numbers: Abstract Image Representations. Proceedings
of SIGGRAPH 90, 207–214.

[6] Hertzmann, A., and Perlin, K. Painterly Rendering for Video and Interaction.
Proceedings of NPAR 2000, 7–12.

[7] Hertzmann, A., and Zorin, D. Illustrating smooth surfaces. Proceedings of
SIGGRAPH 2000, 517–526.

[8] Kaplan, M., Gooch, B., and Cohen, E. Interactive Artistic Rendering.
Proceedings of NPAR 2000, 67–74.

[9] Klein, A., Li, W., Kazhdan, M., Correa, W., Finkelstein, A., and Funkhouser,
T. Non-Photorealistic Virtual Environments. Proceedings of SIGGRAPH 2000,
527–534.

[10] Kowalski, M. A., Markosian, L., Northrup, J. D., Bourdev, L., Barzel, R.,
Holden, L. S., and Hughes, J. Art-Based Rendering of Fur, Grass, and Trees.
Proceedings of SIGGRAPH 99 (August 1999), 433–438.

[11] Lake, A., Marshall, C., Harris, M., and Blackstein, M. Stylized Rendering
Techniques for Scalable Real-Time 3D Animation. Proceedings of NPAR 2000,
13–20.

[12] Litwinowicz, P. Processing Images and Video for an Impressionist Effect.
Proceedings of SIGGRAPH 97, 407–414.

[13] Markosian, L., Kowalski, M. A., Trychin, S. J., Bourdev, L. D., Goldstein, D.,
and Hughes, J. F. Real-Time Nonphotorealistic Rendering. Proceedings of
SIGGRAPH 97, 415–420.

[14] Meier, B. J. Painterly rendering for animation. Proceedings of SIGGRAPH 96,
477–484.

[15] Northrup, J. D., and Markosian, L. Artistic Silhouettes: A Hybrid Approach.
Proceedings of NPAR 2000, 31–38.

[16] Ostromoukhov, V. Digital Facial Engraving. Proceedings of SIGGRAPH 99,
417–424.

[17] Praun, E., Finkelstein, A., and Hoppe, H. Lapped Textures. Proceedings of
SIGGRAPH 2000, 465–470.

[18] Raskar, R., and Cohen, M. Image Precision Silhouette Edges. 1999 ACM
Symposium on Interactive 3D Graphics, 135–140.

[19] Rossl, C., and Kobbelt, L. Line-Art Rendering of 3D Models. Proceedings of
Pacific Graphics 2000.

[20] Saito, T., and Takahashi, T. Comprehensible Rendering of 3D Shapes.
Proceedings of SIGGRAPH 90, 197–206.

[21] Salisbury, M. P., Anderson, S. E., Barzel, R., and Salesin, D. H. Interactive
Pen-And-Ink Illustration. Proceedings of SIGGRAPH 94, 101–108.

[22] Salisbury, M. P., Wong, M. T., Hughes, J. F., and Salesin, D. H. Orientable
Textures for Image-Based Pen-and-Ink Illustration. Proceedings of SIGGRAPH
97, 401–406.

[23] Sander, P., Gu, X., Gortler, S., Hoppe, H., and Snyder, J. Silhouette clipping.
Proceedings of SIGGRAPH 2000, 335–342.

[24] Sousa, M. C., and Buchanan, J.W. Observational Model of Blenders and Erasers
in Computer-Generated Pencil Rendering. Proceedings of Graphics Interface
’99, 157 – 166.

[25] Sousa, M. C., and Buchanan, J. W. Computer-Generated Graphite Pencil Rendering
of 3D Polygonal Models. Computer Graphics Forum 18, 3 (September
1999), 195–208.

[26] Winkenbach, G., and Salesin, D. H. Computer-generated pen-and-ink illustration.
Proceedings of SIGGRAPH 94, 91–100.

[27] Winkenbach, G., and Salesin, D. H. Rendering Parametric Surfaces in Pen and
Ink. Proceedings of SIGGRAPH 96, 469–476.
