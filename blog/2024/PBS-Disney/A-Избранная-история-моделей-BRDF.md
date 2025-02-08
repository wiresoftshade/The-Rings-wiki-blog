## А Избранная история моделей BRDF, используемых в графике

- **Бекманн 1963** [^5] предложил модель рассеяния от шероховатых поверхностей, основанную на гауссовом распределении уклонов поверхности. 
    
    > *Beckmann 1963 provided a model for scattering from rough surfaces based on a Gaussian distribution of surface slopes.*

- **Торранс и Спарроу 1967** [^30] представили модель микрограней. Было принято гауссовское распределение углов микрограней, а фактор затенения микрограней был выведен из упрощающих геометрических предположений.
    
    > *Torrance and Sparrow 1967 introduced the microfacet model. A Gaussian distribution of microfacet angles was assumed and a microfacet shadowing factor was derived from simplifying geometric assumptions.*

- **Смит 1967** [^29] вывел функцию затенения из распределения микрограней. Примечательно, что эта функция затенения менялась в зависимости от шероховатости поверхности.
  
    > *Smith 1967 derived a shadowing function from the microfacet distribution. Notably, this shadowing function varied with surface roughness.*

- **Фонг 1975** [^25] предложил вычислительно простую модель зеркального блика с использованием экспоненциированного косинуса.

    > *Phong 1975 proposed a computationally simple model of a specular highlight using an exponentiated cosine.*

- **Троубридж и Рейц 1975** [^31] вывели новое распределение микрограней на основе средней поверхностной неровности изогнутых микроповерхностей, полученных из эллипсоида вращения. Они подогнали свою модель к измеренным данным для грубого стекла и сравнили свои результаты с распределениями Гаусса, Бекмана, Сирохи и Берри.

    > *Trowbridge and Reitz 1975 derived a new microfacet distribution based on average surface irregularity of curved microsurfaces derived from an ellipsoid of revolution. They fit their model to measured data for rough glass and compared their results with Gaussian, Beckmann, Sirohi, and Berry distributions.*

- **Блинн 1977** [^6] реализовал модель Торранса-Спарроу с распределением Троубриджа-Рейтца (выбранным из-за его вычислительной эффективности, а также его физической основы). Блинн также предложил микрогранное распределение на основе модели Фонга, обычно называемое «Блинн-Фонг», адаптировав его к более физически корректной формулировке полувектора.

    > *Blinn 1977 implemented the Torrance-Sparrow model with the Trowbridge-Reitz distribution (chosen for its computational efficiency as well as its physical basis). Blinn also proposed a microfacet distribution based on the Phong model, commonly referred to as “Blinn Phong,” by adapting it to the more physically correct half-vector formulation.*

- **Кук и Торранс 1981** [^7] реализовали модель Торранса-Спарроу с распределением Бекмана и изучили спектральные сдвиги, обусловленные фактором Френеля.

    > *Cook and Torrance 1981 implemented the Torrance-Sparrow model with the Beckmann distribution and studied spectral shifts due to the Fresnel factor.*

- **Хе, Торранс, Силлион и Гринберг 1991** [^12] представили модель, которая включала зеркальные, направленные диффузные и однородные диффузные компоненты. Модель выведена для поляризованного света и упрощена для неполяризованного света.

    > *He, Torrance, Sillion, and Greenberg 1991 presented a model that included specular, directional diffuse, and uniform diffuse components. The model is derived for polarized light and simplified for unpolarized light.*

- **Уорд 1992** [^34] представил анизотропную зеркальную модель, полученную из распределения Бекмана. **Уолтер 2005** [^32] предоставил более эффективную точную реализацию.

    > *Ward 1992 presented an anisotropic specular model derived from the Beckmann distribution. Walter 2005 provided a more efficient exact implementation.*

- **Льюис 1993** [^16] предложил «модифицированную модель Фонга», которая включала нормализующий член для сохранения энергии.

    > *Lewis 1993 proposed a “modified Phong” model that included a normalization term for energy conservation.*

- **Ханрахан и Крюгер 1993** [^11] разработали диффузную модель BRDF, которая аппроксимирует подповерхностный перенос.

    > *Hanrahan and Krueger 1993 developed a diffuse BRDF model that approximates subsurface transport.*

- **Орен и Наяр 1994** [^23] вывели диффузную модель для шероховатых поверхностей на основе ламбертовских микрограней.

    > *Oren and Nayar 1994 derived a diffuse model for rough surfaces based on Lambertian microfacets.*

- **Шлик 1994** [^28] разработал рациональные аппроксимации для различных компонентов модели микрограней. Широко используется приближение Шлика-Френеля. Кроме того, Шлик распознал разрыв в члене затенения Торранса-Спарроу и предложил приближение функции затенения Смита в качестве альтернативы. Шлик также представил приближение к распределению Бекмана.

    > *Schlick 1994 developed rational approximations to the various components of the microfacet model. The Schlick Fresnel approximation is widely used. Also, Schlick recognized the discontinuity in the Torrance-Sparrow shadowing term and suggested an approximation of the Smith shadowing function as an alternative. Schlick also presented an approximation to the Beckmann distribution.*

- **Лафортюн 1997** [^15] предложил использовать сумму произвольно ориентированных лепестков Фонга в качестве основы для общей модели.

    > *Lafortune 1997 proposed using a sum of arbitrarily oriented Phong lobes as the basis for a general model.*

- **Вольф, Наяр и Орен 1998** [^35] разработали улучшенную диффузную модель для очень гладких поверхностей, которые темнее под углами скольжения, чем диффузия Ламберта из-за эффекта Френеля. Эта модель также объединена в приближенной форме с моделью Орена Наяра для представления континуума гладких и шероховатых диффузных поверхностей.

    > *Wolff, Nayar and Oren 1998 developed an improved diffuse model for very smooth surfaces which are darker at grazing angles than Lambert diffuse due to the Fresnel effect. This model is also combined in an approximate form with the Oren Nayar model to represent a continuum of smooth to rough diffuse surfaces.*

- **Нейман и др. 1999** [^19] предложили модель «растянутого Фонга», предназначенную для металлических поверхностей, альбедо которых становится плоским по мере того, как поверхность становится блестящей.
    
    > *Neumann et al. 1999 proposed a “stretched Phong” model intended for metallic surfaces that has an albedo that becomes flat as the surface becomes shiny.*

- **Нейман и др. 1999b** [^20] предложили процесс «накачки» альбедо произвольных BRDF для улучшения энергетического баланса. Было показано, что предыдущие модели имеют альбедо, которое слишком быстро сходит с углом падения (за исключением модели Уорда, которая, как показано, отклоняется от нормы при скользящем падении). Каждое итеративное накачивание делит BRDF на измеренный поправочный коэффициент, делая альбедо постепенно более плоским.

    > *Neumann et al. 1999b proposed a process to “pump up” the albedo of arbitrary BRDFs to improve energy balance. Previous models were shown to have an albedo that falls off too quickly with incident angle (except for the Ward model which is shown to diverge at grazing incidence). Each iterative pump up divides the BRDF by a measured correction factor making the albedo progressively flatter.*

- **Ашихмин, Преможе и Ширли 2000** [^2] вывели функцию затенения путем численного интегрирования произвольных распределений микрограней.

    > *Ashikhmin, Premože, and Shirley 2000 derived a shadowing function from numeric integration of arbitrary microfacet distributions.*

- **Ашихмин и Ширли 2000** [^3] представили анизотропную модель Фонга, которая включала диффуз с весами Френеля и гарантии сохранения энергии.

    > *Ashikhmin and Shirley 2000 presented a anisotropic Phong model that included a Fresnel-weighted diffuse and energy conservation guarantees.*

- **Келемен и Ширмей-Калос 2001** [^13] предложили альтернативный термин затенения, который аппроксимирует функцию затенения Торранса-Спарроу с дифференцируемой формой. Также предлагается связанно-диффузная модель, так что общее альбедо всегда равно 1.

    > *Kelemen and Szirmay-Kalos 2001 proposed an alternative shadowing term that approximates the Torrance-Sparrow shadowing function with a differentiable form. A coupled-diffuse model is also proposed such that the total albedo is always 1.*

- **Дюр 2006** [^8] улучшил энергетический баланс модели Уорда.

    > *Dür 2006 improved the energy balance of the Ward model.*

- **Эдвардс и др. 2006** [^9] предложили «диск вектора половины пути» в качестве новой области для моделирования зеркальных распределений с целью идеального сохранения энергии (альбедо = 1). Также представлена ​​альтернативная неконсервативная форма для подгонки данных.

    > *Edwards et al. 2006 proposed the “halfway vector disk” as a new domain for modeling specular distributions with the goal of perfect energy conservation (albedo = 1). An alternate non-conservative form is also presented for data fitting.*

- **Ашихмин и Преможе 2007** [^1] представили «распределение BRDF», которое сглаживает разрыв в затеняющем члене Ашихмина Ширли. Также представлен простой метод оценки зеркальных распределений из изображений обратного рассеяния (например, из одной фотографии, освещенной вспышкой).

    > *Ashikhmin  and  Premože  2007  presented  the  “distribution  BRDF”  which  smooths  out  the discontinuity in the shadowing term of Ashikhmin Shirley. A simple method for estimating specular distributions from backscattering images (such as from a single flash-lit photograph) is also provided.*

- **Уолтер и др. 2007** [^33] вывели функции затенения Смита для распределений Фонга и GGX и предоставили приближение затенения Смита для распределения Бекмана. Примечание: GGX эквивалентно распределению Троубриджа-Рейтца.

    > *Walter et al. 2007 derived Smith shadowing functions for the Phong and GGX distributions and provided an approximation of Smith shadowing for the Beckmann distribution. Note: GGX is equivalent to the Trowbridge-Reitz distribution.*

- **Ромейро и др. 2008** [^26] показали, что материалы MERL хорошо представлены простой двумерной формой $ρ(θ_h, θ_d)$, и использовали этот факт, чтобы предложить упрощенный метод захвата BRDF.

    > *Romeiro et al. 2008 showed than the MERL materials are well-represented by a simple bivariate form, $ρ(θ_h, θ_d)$ and exploited this fact to proposed a simplified BRDF capture method.*

- **Гейслер-Мородер и Дюр 2010** [^10] дополнительно усовершенствовали эту модель, чтобы восстановить взаимность Гельмгольца и гарантировать сохранение энергии.

    > *Geisler-Moroder  and  Dür  2010 further  refined  this  model  to  restore  Helmholtz  reciprocity and guarantee energy conservation.*

- **Курт и др. 2010** [^14] расширили распределение Бекмана до анизотропной формы и предложили новую параметризованную функцию затенения, дающую контроль над альбедо и улучшающую подгонку для некоторых материалов. Для подгонки многих материалов MERL предлагается использовать два зеркальных лепестка.

    > *Kurt et al. 2010 extended the Beckmann distribution to anisotropic form and proposed a new parameterized shadowing function giving control over albedo and improving fitting for some materials. Two specular lobes are suggested for fitting many of the MERL materials.*

- **Нишино и Ломбарди 2011** [^22] предложили «полусферическое экспоненциальное распределение мощности» или «Hemi-EPD», которое имеет дополнительную степень свободы для улучшения мощности подгонки. Hemi-EPD используется в качестве основы для всего BRDF, а параметры подгоняются под отдельные $θ_d$ срезы и интерполируются. Кроме того, требуется несколько лепестков на срез $θ_d$ для многих материалов.
  
    > *Nishino and Lombardi 2011 proposed the “hemispherical exponential power distribution” or “Hemi-EPD” which has an additional degree of freedom to improve fitting power. The Hemi- EPD is used as a basis for the entire BRDF and parameters are fit to individual $θ_d$ slices and interpolated. Additionally, multiple lobes per $θ_d$ slice are required for many materials.*

- **Лёв и др. 2012** [^17] предложили новое распределение микрограней «ABC», вдохновленное теорией рассеяния гладких поверхностей Рэлея-Райса. Кроме того, «проецируемый вектор отклонения» представлен как альтернатива параметризации полувектора для подгонки данных.
  
    > *Löw  et  al.   2012   proposed  a  new  “ABC”  microfacet  distribution  inspired  by  Rayleigh-Rice smooth-surface scattering theory. Additionally, the “projected deviation vector” is presented as an alternative to the half-vector parameterization for data fitting.*

- **Пакановски и др. 2012** [^24] разработали структуру для подгонки рациональных функций к общим изотропным BRDF в области $(θ_h, θ_d)$. Анизотропная форма также предлагается как простое масштабирование изотропной формы относительно $φ_h$.

    > *Pacanowski et al. 2012 developed a framework for fitting rational functions to general isotropic BRDFs over the $(θ_h, θ_d)$ domain. An anisotropic form is also proposed as a simple scaling of the isotropic form with respect to $φ_h$.*

- **Багер и др. 2012** [^4] предложили новое распределение микрограней «смещенной гаммы» или «SGD», полученное для подгонки под диапазон наблюдаемых наклонов в базе данных MERL. Приведена аппроксимация функции затенения Смита для SGD. Кроме того, член Френеля модифицирован с помощью поправочного члена, обеспечивающего дополнительную степень свободы, что улучшает подгоночную способность.

    > *Bagher et al. 2012 proposed a new “shifted gamma” or “SGD” microfacet distribution derived to fit the range of observed slopes in the MERL database. An approximation of the Smith shadowing function for the SGD is provided. Additionally, the Fresnel term is modified with a correction term providing an additional degree of freedom, improving fitting ability.*

[^1]: Michael Ashikhmin. Distribution-based brdfs. Technical report, 2007.

[^2]: Michael Ashikhmin, Simon Premože, and Peter Shirley.  A Microfacet-Based BRDF generator.  In Sheila Hoffmeyer, editor, Proceedings of the Computer Graphics Conference 2000 (SIGGRAPH-00), pages 65–74, New York, July 23–28 2000. ACMPress.

[^3]: Michael Ashikhmin and Peter Shirley. An anisotropic Phong BRDF model. Journal of Graphics Tools: JGT, 5(2):25–32, 2000.

[^4]: M. M. Bagher, C. Soler, and N. Holzschuch. Accurate fitting of measured reflectances using a shifted gamma micro-facet distribution. Computer Graphics Forum, 31(4):1509–1518, 2012.

[^5]: P. Beckmann and A. Spizzichino. The scattering of electromagnetic waves from rough surfaces. MacMillan, 1963.

[^6]: James F. Blinn. Models of light reflection for computer synthesized pictures. volume 11, pages 192–198, July 1977.

[^7]: R. L. Cook and K. E. Torrance. A reflectance model for computer graphics. Computer Graphics, 15(3):307–316, 1981.

[^8]: Arne Dür.  An improved normalization for the Ward reflectance model.  Journal  of  graphics,  gpu, and game tools, 11(1):51–59, 2006.

[^9]: Dave Edwards, Solomon Boulos, Jared Johnson, Peter Shirley, Michael Ashikhmin, Michael Stark, and Chris Wyman. The halfway vector disk for brdf modeling. ACM Trans. Graph., 25(1):1–18, January 2006.

[^10]: David Geisler-Moroder and Arne Dür.  A new Ward BRDF model with bounded albedo.  Comput. Graph. Forum, 29(4):1391–1398, 2010.

[^11]: Pat Hanrahan and Wolfgang Krueger. Reflection from layered surfaces due to subsurface scatter- ing. In Proceedings of the 20th annual conference on Computer graphics and interactive techniques, SIGGRAPH ’93, pages 165–174, New York, NY, USA, 1993. ACM.

[^12]: Xiao D. He, Kenneth E. Torrance, Francois X. Sillion, and Donald P. Greenberg. A Comprehensive Physical Model for Light Reflection. In Computer Graphics (ACM SIGGRAPH ’91 Proceedings), volume 25, pages 175–186, July 1991.

[^13]: Csaba  Kelemen,  Laszlo  Szirmay-Kalos,  and  L´aszl´o  Szirmay-kalos.   A  microfacet  based  coupled specular-matte brdf model with importance sampling. Eurographics Short Presentations, 2001.

[^14]: Murat Kurt, L´aszl´o Szirmay-Kalos, and Jaroslav Kˇriv´anek.  An anisotropic brdf model for fitting and monte carlo rendering. SIGGRAPH Comput. Graph., 44(1):3:1–3:15, February 2010.

[^15]: Eric P. Lafortune, Sing-Choong Foo, Kenneth E. Torrance, and Donald P. Greenberg.  Non- linear approximation of reflectance functions. In Computer Graphics (ACM SIGGRAPH ’97 Proceedings), volume 31, pages 117–126, 1997.

[^16]: Robert R. Lewis. Making Shaders More Physically Plausible. In Fourth Eurographics Workshop on Rendering, number Series EG 93 RW, pages 47–62, Paris, France, June 1993.

[^17]: Joakim Löw, Joel Kronander, Anders Ynnerman, and Jonas Unger.  Brdf models for accurate and efficient rendering of glossy surfaces. ACM Trans. Graph., 31(1):9:1–9:14, February 2012.

[^18]: Wojciech Matusik, Hanspeter Pfister, Matt Brand, and Leonard McMillan. A data-driven re- flectance model. ACM Transactions on Graphics, 22(3):759–769, July 2003.

[^19]: L´aszl´o Neumann, Attila Neumann, and L´aszl´o Szirmay-Kalos.  Compact metallic reflectance mod- els. Computer Graphics Forum, 18(3):161–172, September 1999. ISSN 1067-7055.

[^20]: L´aszl´o  Neumann,  Attila  Neumann,  and  L´aszl´o  Szirmay-Kalos.   Reflectance  models  by  pumping up the albedo function. In Machine Graphics and Vision, pages 3–18, 1999.

[^21]: Addy  Ngan,  Fr´edo  Durand,  and  Wojciech  Matusik.  Experimental  analysis  of  BRDF  models.  In Kavita  Bala  and  Philip  Dutr´e,  editors,  Eurographics  Symposium  on  Rendering,  pages  117–126, Konstanz, Germany, 2005. Eurographics Association.

[^22]: Ko Nishino and Stephen Lombardi. Directional statistics-based reflectance model for isotropic bidirectional reflectance distribution functions. J. Opt. Soc. Am. A, 28(1):8–18, Jan 2011.

[^23]: Michael Oren and Shree K. Nayar. Generalization of lambert’s reflectance model. In SIGGRAPH, pages 239–246. ACM, 1994.

[^24]: Romain Pacanowski, Oliver Salazar Celis, Christophe Schlick, Xavier Granier, Pierre Poulin, and Annie Cuyt. Rational brdf. IEEE Transactions on Visualization and Computer Graphics, 99(PrePrints), 2012.

[^25]: Bui-T. Phong. Illumination for computer generated pictures. Communications of the ACM, 18(6):311–317, June 1975.

[^26]: Fabiano Romeiro, Yuriy Vasilyev, and Todd Zickler. Passive reflectometry. In Proceedings of the 10th European Conference on Computer Vision: Part IV, ECCV ’08, pages 859–872, Berlin, Heidelberg, 2008. Springer-Verlag.

[^27]: Iman Sadeghi, Heather Pritchett, Henrik Wann Jensen, and Rasmus Tamstorf. An artist friendly hair shading system. In ACM SIGGRAPH 2010 papers, SIGGRAPH ’10, pages 56:1–56:10, New York, NY, USA, 2010. ACM.

[^28]: Christophe Schlick. An Inexpensive BRDF Model for Physically-Based Rendering. Computer Graphics Forum, 13(3):233–246, 1994.

[^29]: B. Smith. Geometrical shadowing of a random rough surface. IEEE Trans. Ant. and Propagation, AP-15(5):668–671, September 1967.

[^30]: K. Torrance and E. Sparrow. Theory for off-specular reflection from roughened surfaces. J. Optical Soc. America, 57:1105–1114, 1967.

[^31]: S. Trowbridge and K. P. Reitz. Average irregularity representation of a rough ray reflection.
Journal of the Optical Society of America, 65(5):531–536, May 1975.

[^32]: Bruce Walter. Notes on the Ward BRDF. Technical Report PCG-05-06, Cornell Program of Computer Graphics, 2005.

[^33]: Bruce Walter, Stephen R. Marschner, Hongsong Li, and Kenneth E. Torrance. Microfacet models for refraction through rough surfaces. In Proceedings of the Eurographics Symposium on Rendering, 2007.

[^34]:  Gregory J. Ward. Measuring and modeling anisotropic reflection. In Edwin E. Catmull, editor,
*Computer Graphics (SIGGRAPH ’92 Proceedings)*, volume 26, pages 265–272, July 1992.

[^35]: L. B. Wolff, S. K. Nayar, and M. Oren. Improved diffuse reflection models for computer vision.
*International Journal of Computer Vision*, 30(1):55–71, October 1998.