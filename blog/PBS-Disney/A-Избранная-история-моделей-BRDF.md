## А Избранная история моделей BRDF, используемых в графике

- Beckmann 1963 [5] provided a model for scattering from rough surfaces based on a Gaussian distribution of surface slopes.

- Torrance and Sparrow 1967 [30] introduced the microfacet model. A Gaussian distribution of microfacet angles was assumed and a microfacet shadowing factor was derived from simplifying geometric assumptions.

- Smith 1967 [29] derived a shadowing function from the microfacet distribution. Notably, this shadowing function varied with surface roughness.

- Phong 1975 [25] proposed a computationally simple model of a specular highlight using an ex-ponentiated cosine.

- Trowbridge and Reitz 1975 [31] derived a new microfacet distribution based on average surface irregularity of curved microsurfaces derived from an ellipsoid of revolution. They fit their model to measured data for rough glass and compared their results with Gaussian, Beckmann, Sirohi, and Berry distributions.

- Blinn 1977 [6] implemented the Torrance-Sparrow model with the Trowbridge-Reitz distribution (chosen for its computational efficiency as well as its physical basis). Blinn also proposed a microfacet distribution based based on the Phong model, commonly referred to as “Blinn Phong,” by adapting it to the more physically correct half-vector formulation.

- Cook and Torrance 1981 [7] implemented the Torrance-Sparrow model with the Beckmann dis- tribution and studied spectral shifts due to the Fresnel factor.

- He, Torrance, Sillion, and Greenberg 1991 [12] presented a model that included specular, di- rectional diffuse, and uniform diffuse components. The model is derived for polarized light and simplified for unpolarized light.

- Ward 1992 [34] presented an anisotropic specular model derived from the 

- Beckmann distribution. Walter 2005 [32] provided a more efficient exact implementation.

- Lewis 1993 [16] proposed a “modified Phong” model that included a normalization term for energy conservation.

- Hanrahan and Krueger 1993 [11] developed a diffuse BRDF model that approximates subsurface transport.

- Oren and Nayar 1994 [23] derived a diffuse model for rough surfaces based on Lambertian mi- crofacets.

- Schlick 1994 [28] developed rational approximations to the various components of the microfacet model. The Schlick Fresnel approximation is widely used. Also, Schlick recognized the discon- tinuity in the Torrance-Sparrow shadowing term and suggested an approximation of the Smith shadowing function as an alternative. Schlick also presented an approximation to the Beckmann distribution.

- Lafortune 1997 [15] proposed using a sum of arbitrarily oriented Phong lobes as the basis for a general model.

- Wolff, Nayar and Oren 1998 [35] developed an improved diffuse model for very smooth surfaces which are darker at grazing angles than Lambert diffuse due to the Fresnel effect. This model is also combined in an approximate form with the Oren Nayar model to represent a continuum of smooth to rough diffuse surfaces.

- Neumann et al. 1999 [19] proposed a “stretched Phong” model intended for metallic surfaces that has an albedo that becomes flat as the surface becomes shiny.

- Neumann et al. 1999b [20] proposed a process to “pump up” the albedo of arbitrary BRDFs to improve energy balance. Previous models were shown to have an albedo that falls off too quickly with incident angle (except for the Ward model which is shown to diverge at grazing incidence). Each iterative pump up divides the BRDF by a measured correction factor making the albedo progressively flatter.

- Ashikhmin, Premoˇze, and Shirley 2000 [2] derived a shadowing function from numeric integration of arbitrary microfacet distributions.

- Ashikhmin and Shirley 2000 [3] presented a anisotropic Phong model that included a Fresnel- weighted diffuse and energy conservation guarantees.

- Kelemen and Szirmay-Kalos 2001 [13] proposed an alternative shadowing term that approximates the Torrance-Sparrow shadowing function with a differentiable form. A coupled-diffuse model is also proposed such that the total albedo is always 1.

- Du¨r 2006  [8] improved  the energy  balance  of the Ward model.

- Edwards et al. 2006 [9] proposed the “halfway vector disk” as a new domain for modeling specular distributions with the goal of perfect energy conservation (albedo = 1). An alternate non-conservative form is also presented for data fitting.

- Ashikhmin  and  Premoˇze  2007  [1]  presented  the  “distribution  BRDF”  which  smooths  out  the discontinuity in the shadowing term of Ashikhmin Shirley. A simple method for estimating specular distributions from backscattering images (such as from a single flash-lit photograph) is also provided.

- Walter et al. 2007 [33] derived Smith shadowing functions for the Phong and GGX distributions and provided an approximation of Smith shadowing for the Beckmann distribution. Note: GGX is equivalent to the Trowbridge-Reitz distribution.

- Romeiro et al. 2008 [26] showed than the MERL materials are well-represented by a simple bivariate form, $ρ(θ_h, θ_d)$ and exploited this fact to proposed a simplified BRDF capture method.

- Geisler-Moroder  and  Du¨r  2010  [10]  further  refined  this  model  to  restore  Helmholtz  reciprocity and guarantee energy conservation.

- Kurt et al 2010 [14] extended the Beckmann distribution to anisotropic form and proposed a new parameterized shadowing function giving control over albedo and improving fitting for some materials. Two specular lobes are suggested for fitting many of the MERL materials.

- Nishino and Lombardi 2011 [22] proposed the “hemispherical exponential power distribution” or “Hemi-EPD” which has an additional degree of freedom to improve fitting power. The Hemi- EPD is used as a basis for the entire BRDF and parameters are fit to individual $θ_d$ slices and interpolated. Additionally, multiple lobes per $θ_d$ slice are required for many materials.

- L¨ow  et  al.   2012  [17]  proposed  a  new  “ABC”  microfacet  distribution  inspired  by  Rayleigh-Rice smooth-surface scattering theory. Additionally, the “projected deviation vector” is presented as an alternative to the half-vector parameterization for data fitting.

- Pacanowski et al. 2012 [24] developed a framework for fitting rational functions to general isotropic BRDFs over the $(θ_h, θ_d)$ domain. An anisotropic form is also proposed as a simple scaling of the isotropic form with respect to $φ_h$.

- Bagher et al. 2012 [4] proposed a new “shifted gamma” or “SGD” microfacet distribution derived to fit the range of observed slopes in the MERL database. An approximation of the Smith shadowing function for the SGD is provided. Additionally, the Fresnel term is modified with a correction term providing an additional degree of freedom, improving fitting ability.
