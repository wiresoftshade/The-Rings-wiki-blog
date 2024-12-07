GitHub: Базовый синтаксис записи и форматирования
---------------------------

Создавайте расширенное форматирование текста и кода в GitHub с помощью простого синтаксиса

[docs.github.com/ru/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax](https://docs.github.com/ru/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

Headers
---------------------------

# Header 1

## Header 2

### Header 3

#### Header 4

##### Header 5

###### Header 6

####### Header 7

Styling
---------------------------

*Emphasize* _emphasize_

**Strong** __strong__

~~Mistaken text.~~

***Strong and emphasize***

> Quoted text.

Normal text <sub>subscript text</sub> 

Normal text <sup>superscript text</sup>

Lists
---------------------------

- Item
  * Item
    + Item

1. Item 1
2. Item 2
3. Item 3

- [ ] Incomplete item
- [x] Complete item



Links
---------------------------

A [link](http://example.com).

An image: ![Alt](img.jpg)

A sized image: ![Alt](img.jpg =60x50)



Code
---------------------------

Some `inline code`.

    // A code block by tabs
    var foo = 'bar';


```
// A code block
var foo = 'bar';
```

```javascript
// An javascript highlighted block
var foo = 'bar';
```

```tex
% An LaTeX (math) highlighted block
$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$
```

```hlsl
// An HLSL highlighted block
float3 RGBcolor(float r, float g, float b)
{
  return float3(r,g,b);
}
```

Оповещения
---------------------------

Оповещения — это расширение Markdown на основе синтаксиса blockquote, который можно использовать для выделения критически важных сведений. На GitHub они отображаются с отличительными цветами и значками, чтобы указать важность содержимого.

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.

https://docs.github.com/ru/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts

Comments
---------------------------

<!-- This content will not appear in the rendered Markdown -->

```
<!-- This content will not appear in the rendered Markdown -->
```


Tables
---------------------------

Item     | Value
-------- | -----
Computer | $1600
Phone    | $12
Pipe     | $1


| Column 1 | Column 2      |
|:--------:| -------------:|
| centered | right-aligned |


Footnotes
---------------------------

Some text with a footnote.[^1]

[^1]: The footnote.

LaTeX math
---------------------------

The Gamma function satisfying $\Gamma(n) = (n-1)!\quad\forall
n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

