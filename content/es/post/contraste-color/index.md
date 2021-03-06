---
title: Contraste de color
subtitle: Sobre blanco y negro *a la vez*
summary: Contraste de color sobre blanco y negro *a la vez*.
date: "2020-09-05T00:00:00Z"
authors:
- rodrigo-alcaraz-de-la-osa
tags:
- color
image:
  placement: 3  
  caption: Foto de [**Paweł Czerwiński**](https://unsplash.com/@pawel_czerwinski) en [Unsplash](https://unsplash.com)
---

{{% alert note %}}
Esta entrada es una **traducción/adaptación/ampliación** del [**excelente artículo** de **Ben Szabo** en dev.to](https://dev.to/finnhvman/which-colors-look-good-on-black-and-white-2pe6).
{{% /alert %}}

Estoy planteándome la posibilidad de permitir elegir a los visitantes de mi web si desean un **fondo claro** u **oscuro**. Con un fondo oscuro (casi negro) el texto pasaría a ser claro (casi blanco), a la inversa de como es actualmente, pero el **color** de **resalte**, este azul <svg width="1rem" height="1rem">
  <rect rx="4" ry="4" width="1rem" height="1rem" style="fill:#2a54a9" />
</svg>, dejaría de tener suficiente **contraste** sobre el negro.

## ¿Qué es el contraste y cómo se define?
Las *Pautas de Accesibilidad para el Contenido Web*, [**WCAG**](https://www.w3.org/WAI/standards-guidelines/wcag/es) por sus siglas en inglés, [definen la relación de **contraste**](https://www.w3.org/TR/WCAG21/#dfn-contrast-ratio), $C$, como:

$$
C = \frac{L1 + 0.05}{L2 + 0.05},
$$

donde $L1$ y $L2$ son las *luminosidades relativas* de los colores claro y oscuro, respectivamente. La [luminosidad relativa](https://www.w3.org/TR/WCAG21/#dfn-relative-luminance) se define a su vez como:

> El brillo relativo de cualquier punto en un espacio de color, normalizado a 0 para el negro más oscuro y 1 para el blanco más claro.

En el caso del espacio de color **sRGB**, el utilizado por defecto en toda la Web, existen unas [expresiones *sencillas* para calcular esta luminosidad relativa](https://www.w3.org/TR/WCAG21/#dfn-relative-luminance), que depende de las coordenadas del color en cuestión.

El negro tiene una luminosidad relativa igual a 0, mientras que la del blanco es igual a 1, por lo que el **máximo contraste posible**, $C_\text{máx}$, es[^1]:

[^1]: Como el blanco es más claro que el negro, su luminosidad, 1, va en el numerador, mientras que la del negro, 0, va en el denominador.

$$
C_\text{máx} = \frac{1+0.05}{0+0.05} = 21
$$

Las pautas WCAG nos dicen que la relación de **contraste mínimo** entre un texto y su fondo debería ser de al menos **4.5:1**.

{{% alert note %}}

[Colorable](https://colorable.jxnblk.com/) es una excelente herramienta con la que podemos comprobar el contraste de combinaciones de colores.

{{% /alert %}}

## Entonces, ¿qué colores se ven bien tanto sobre blanco como sobre negro?
Dada la luminosidad relativa de un color, $L$, podemos calcular su **contraste sobre blanco**, $C_\text{blanco}$, con la expresión[^2]:

[^2]: Como el blanco es el color más claro, $L$ va en el denominador.

$$
C_\text{blanco} = \frac{1 + 0.05}{L + 0.05} = \frac{1.05}{L+0.05}
$$

El **contraste sobre negro**, $C_\text{negro}$, lo calculamos con la expresión[^3]:

[^3]: Ahora será el color en cuestión el color más claro ($L$ en el numerador), pues el negro es el color más oscuro.

$$
C_\text{negro} = \frac{L + 0.05}{0 + 0.05} = \frac{L+0.05}{0.05}
$$

Si queremos elegir un color que se vea bien tanto sobre blanco como sobre negro, debemos imponer que ambos contrastes, $C_\text{blanco}$ y $C_\text{negro}$, sean como mínimo iguales a 4.5. Eso nos da estas dos <strong>inecuaciones</strong>:

\begin{align*}
C_\text{blanco} &= \frac{1.05}{L+0.05} \geq 4.5 \tag{1} \\\\
C_\text{negro} &= \frac{L+0.05}{0.05} \geq 4.5 \tag{2}
\end{align*}

De la primera (**blanco**) sacamos:

$$
L \leq \frac{1.05}{4.5}-0.05 = 0.18\overline{3},
$$

mientras que de la segunda (**negro**):

$$
L \geq 4.5\cdot 0.05-0.05 = 0.175
$$

Por lo que $0.175\leq L\leq 0.18\overline{3}$.

[Ben Szabo](https://dev.to/finnhvman) ha creado este *Pen* que itera a través del espacio de color sRGB, con incrementos de 17 por canal[^4], listando **76 colores** cuyo contraste sobre blanco y negro *a la vez* es de 4.5 como mínimo.

[^4]: En el [espacio de color **RGB**](https://es.wikipedia.org/wiki/RGB), los valores de cada canal (rojo, verde y azul) varían desde 0 hasta 255. Incrementos de 17 permiten iterar a través de los colores que pueden ser descritos con una [notación hexadecimal](https://es.wikipedia.org/wiki/Colores_web) de 3 dígitos. Si iteráramos por todos los posibles colores (incrementos de 1) obtendríamos ~300k colores.

<p class="codepen" data-height="600" data-theme-id="light" data-default-tab="result" data-user="finnhvman" data-slug-hash="bZQLgR" style="height: 600px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Colors With 4.5:1 Contrast on Black and White">
  <span>See the Pen <a href="https://codepen.io/finnhvman/pen/bZQLgR">
  Colors With 4.5:1 Contrast on Black and White</a> by Ben Szabo (<a href="https://codepen.io/finnhvman">@finnhvman</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## ¿Cuál es el máximo contraste que podemos conseguir sobre blanco y negro *a la vez*?
Para poder tener suficiente contraste sobre blanco y negro *a la vez*, la luminosidad relativa del color tiene que estar entre dos valores[^5], como se puede ver con las inecuaciones (1) y (2). El **contraste máximo teórico** de un color **sobre blanco** y **negro *a la vez***, $C_\text{b\&n}^\text{máx}$, se puede obtener imponiendo que esos dos valores de luminosidad relativa se igualen:

[^5]: Dicho de otra forma, el color no tiene que ser ni muy claro (pobre contraste sobre blanco) ni muy oscuro (pobre contraste sobre negro).

$$
\frac{1.05}{C_\text{b\&n}^\text{máx}}-\cancel{0.05} = C_\text{b\&n}^\text{máx}\cdot 0.05-\cancel{0.05},
$$

de donde se obtiene $C_\text{b\&n}^\text{máx} = \sqrt{21} \approx 4.58$, que corresponde con este color <strong><em>fucsia</em></strong>:

<ul style="display: grid;
  grid-template-columns: repeat(auto-fill, minmax(1fr, 1fr));
  grid-gap: 16px;
  padding-right: 32px;">
  <li style="border-radius: 4px;
  padding: 48px 16px 16px;
  list-style: none;
  text-align: end; background-color: #cf0dcc; font-family: Inconsolata">
	  <span style="color:white">#cf0dcc</span><br>rgb(207,13,204)
  </li>
</ul>

Una buena **combinación** de **colores primarios** (rojo, verde y azul) sería[^6]:

[^6]: Los tres con un contraste cercano al **máximo teórico** de $\sqrt{21}$ tanto sobre blanco como sobre negro.

<ul style="display: grid;
  grid-template-columns: repeat(auto-fill, minmax(164px, 1fr));
  grid-gap: 16px;
  padding-right: 32px;">
  <li style="border-radius: 4px;
  padding: 48px 16px 16px;
  list-style: none;
  text-align: end; background-color: #e62101; font-family: Inconsolata">
	  <span style="color:white">#e62101</span><br>rgb(230,33,1)
  </li>
  <li style="border-radius: 4px;
  padding: 48px 16px 16px;
  list-style: none;
  text-align: end; background-color: #038901; font-family: Inconsolata">
	  <span style="color:white">#038901</span><br>rgb(3,137,1)
  </li>
  <li style="border-radius: 4px;
  padding: 48px 16px 16px;
  list-style: none;
  text-align: end; background-color: #2f72de; font-family: Inconsolata">
	  <span style="color:white">#2f72de</span><br>rgb(47,114,222)
  </li>    
</ul>