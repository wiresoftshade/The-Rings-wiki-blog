# LATEX Mathematical Symbols 

[A Source full docement in PDF](./additional/LaTeX_symbols.pdf)

The more unusual symbols are not defined in base LATEX (NFSS) and require `\usepackage{amssymb}` 

## 1 GreekandHebrew letters 

α `\alpha` κ `\kappa` ψ `\psi` z `\digamma` ∆ `\Delta` Θ `\Theta` β `\beta` λ `\lambda` ρ `\rho` ε `\varepsilon` Γ `\Gamma` Υ `\Upsilon` χ `\chi` µ `\mu` σ `\sigma` κ `\varkappa` Λ `\Lambda` Ξ `\Xi` δ `\delta` ν `\nu` τ `\tau` ϕ `\varphi` Ω `\Omega` ϵ `\epsilon` o `o` θ `\theta` ϖ `\varpi` Φ `\Phi` ℵ `\aleph` η `\eta` ω `\omega` υ `\upsilon` ϱ `\varrho` Π `\Pi` ℶ `\beth` γ `\gamma` φ `\phi` ξ `\xi` ς `\varsigma` Ψ `\Psi` ℸ `\daleth` ι `\iota` π `\pi` ζ `\zeta` ϑ `\vartheta` Σ `\Sigma` ג `\gimel`

## 2 LATEX math constructs

$\frac{abc}{xyz}\qquad$`\frac{abc}{xyz}`

$f’\qquad$ `f’`

$\sqrt{abc}\qquad$ `\sqrt{abc}`

$\sqrt[n]{abc}\qquad$`\sqrt[n]{abc}`

## 5 Standard Function Names

Function names should appear in Roman, not Italic, e.g., 

Correct: `\tan(at-n\pi)` $\longrightarrow\quad\tan(at − n\pi)$

Incorrect: `tan(at-n\pi)` $\longrightarrow\quad{tan}(at−n\pi)$

## 7 Arrow symbols

$\longrightarrow\qquad$ `\longrightarrow`

## 8 Miscellaneous symbols

$\infty\qquad$`\infty`

## 9 Math mode accents

$\acute{a}\qquad$`\acute{a}`

$\grave{a}\qquad$`\grave{a}`

$\bar{a}\qquad$`\bar{a}`

$\dot{a}\qquad$`\dot{a}`

$\ddot{a}\qquad$`\ddot{a}`

$\vec{a}\qquad$`\vec{a}`

## 12 Text Style

Monospace font: $\mathtt{ABCDEFabcdef123456}\qquad$`\mathtt{ABCDEFabcdef123456}`

Bold font (use for Vectors): $\mathbf{ABCDEFabcdef123456}\qquad$`\mathbf{ABCDEFabcdef123456}`

# Специальная команда указания пробела

`\quad` - это пробел, равный текущему размеру шрифта. Так, если вы используете шрифт размером 11pt, то пространство, предоставляемое `\quad`, также будет равно 11pt (по горизонтали, конечно). `\qquad` дает вдвое больше.

В этой ситуации `\quad` было бы излишним - в данном случае нужны небольшие пробелы

`\,`	small space	 3/18 of a quad

`\:`	medium space	4/18 of a quad

`\;`	large space	    5/18 of a quad

`\!`	negative space	-3/18 of a quad