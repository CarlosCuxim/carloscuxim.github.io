---
title: 'Mi aventura creando un blog'
published: 2025-08-17
draft: false
description: 'El va y ven para crear un blog con la menor cantidad de esfuerzo posible'
tags: ['random']
---

Bueno, este debería ser la primera entrada de mi blog. Desde hace hace rato
tenía planeado crear un blog para simplemente plasmar todas las ideas que me
pasan por la cabeza.

El problema no fue tanto crearlo, hay muchas formas, la idea original era
simplemente usar un script de Python para convertir archivos de markdown en
archivos html con una plantilla ya establecida. Otra opción era simplemente
usar html puro (de hecho tenía ya algo así, pero no duró mucho). El mayor
problema no era programarlo, sino que cada vez que quería algo nuevo, como
incluir matemáticas, un tag para escribir código, un estilo predeterminado
de css, etc., tenía que parar de escribir la entrada en el blog, hacer los
cambios y finalmente seguir escribiendo. Esto hacía que una simple entrada
tomara horas.

Al final me harté. Pero al seguir buscando vi que existen generadores de
html estáticos, donde basta con escribir un `.md` y este genera un sitio con
los enlaces respectivos. Es prácticamente lo que quería hacer con el script
de Python. Y bueno, soy de los que piensan que no es necesario reinventar la
rueda (a menos que eso sea lo que quieras).

Con el plan de usar un generador de sitios estáticos había dos incógnitas que
debía resolver. La primera es ¿Dónde se guardará el sitio? En otras palabras,
¿Cuál debería ser el host? Tenía dos opciones, la primera es usar el VPS que
estoy actualmente rentando y usar el [dominio que estoy rentando](cuxim.com).
Esta no es una mala opción, casi no tengo procesos en el VPS por lo que no
sería un mal uso. Aunque no es muy complejo, si se tiene que configurar los
puertos, los certificados SSL y la forma de hacer deploy (dado que el VPS está
en Europa el ping es lo suficientemente malo como para que editar ahí se
sienta como una tortura).

De esta forma, lo que decidí fue simplemente aprovecharme de GitHub Pages que
hace todo ese proceso por mi. Simplemente necesito clonar el repositorio, hacer
un push y listo, debería estar funcionando.

El problema viene con la segunda cuestión que debía resolver ¿Cuál generador
de sitios usar? El plan iniciar era usar Jekyll, viene nativo con GitHub y hay
varios tutoriales para hacerlo. No es una mala opción, pero decidí buscar otras
opciones. De hecho, dependiendo de la opción que buscara tendría que descartar
la opción de usar GitHub Pages. Sin embargo, para mi sorpresa GitHub tiene una
mejor forma de generar sus páginas además de la nativa con Jekyll, esta es
mediante [GitHub Actions](https://docs.github.com/en/actions). La verdad es
que no se muy bien como funciona, traté de leer la documentación, pero mi
comprensión lectora (al nivel de un niño de primaria) no me dejó claro lo que
debía hacer.

En foros de Reddit vi las diferentes opciones que ofrecía GitHub Actions, de
las cuales tres me parecieron interesantes: Jekyll por que es la forma más
sencilla, Hugo que parece bastante rápido y práctico y finalmente Astro. Me
decanté po este último ya que parece tener la mayor cantidad de personalización
disponible, aparte de tener un [tutorial específico para GitHub Pages](https://docs.astro.build/en/guides/deploy/github/).

Este es el punto en el que estoy ahora mismo. El objetivo de esta primera
entrada es simplemente narrar todos los pasos que estoy siguiendo para que
este blog funcione al menos con esta única entrada. Para mayor contexto, estoy
trabajando en una laptop de bastantes precarias características (un Intel
Celeron con 4 GB de ram) en una instalación (casi) nueva de Arch Linux. Este
no es un sistema operativo con el que suela trabajar a menudo, pero de nada
se aprende con la comodidad.

El primer problema que estoy observando, es que el tutorial asume que ya
tienes un proyecto de Astro, por lo que toca regresar al tutorial de como
instalarlo y usarlo. En primer lugar está el [tutorial para instalarlo](https://docs.astro.build/en/install-and-setup/).

La instalación fue relativamente rápida, simplemente usando `npm` y siguiendo
las instrucciones del instalador. Bueno, o al menos así pensé que era, cuando
intenté correr el comando `npm run dev` apareció el siguiente mensaje.

```log
> carloscuxim-github-io@0.0.1 dev
> astro dev

sh: line 1: astro: command not found
```

Por supuesto no todo podía salir bien. Creo que es una regla no escrita de la
programación (y las matemáticas) que si algo parece salir demasiado bien,
probablemente se rompa en algún momento.

La cuestión es que el mensaje me hace sospechar de que me hace algún programa
para instalar, quiero decir, es bastante claro que me indica que el comando
`astro` se trata de ejecutar pero el shell no lo puede encontrar. Bueno,
después de un rato buscando en google que pasaba, me encontré con varias
soluciones. En primer lugar instalar astro de manera global con `npm`, no es
una mala solución, pero con node prefiero no instalar nada de manera global,
más que nada por que una de las cosas que hacen interesantes a node es que
permite tener un 'entorno virtual' en el que todo está bien empaquetado y
sin dependencias externas. La segunda opción era instalarlo de manera local
y cambiar el script `run` para que lo ejecutara a través de `npx`, tampoco es
una mala opción, pero no se si otras partes del la documentación asumen que
astro estaba instalado de manera global, por lo que es mi última opción.
Afortunadamente la solución era más tonta de lo que pensé, simplemente fue
volver a correr `npm install`, no se si algo no se instaló bien usando el
asistente de creación, pero bueno, al final es una nota a tener en cuenta
que es posible que se tenga que volver a instalar las dependencias.

Bueno, después de un rato leyendo la documentación creo que cometí un gran
error, no es para nada amigable. Parece que usa una estructura de componentes
similar a la de React o Vue.js. Sinceramente no estoy seguro de donde está
cada cosa. Pero, parece que tengo una segunda oportunidad. Al parecer hay un
tutorial enfocado a la [creación de un blog](https://docs.astro.build/en/tutorial/0-introduction/),
chance ahí consiga un buen inicio del cual partir si quiero algo más avanzado.

Creo que voy entendiendo la vaina. Cuando creas un proyecto en astro tienes
una carpeta llamada `src/pages` donde está cada una de las páginas que se van
a renderizar. La página raíz está guardada en `index.astro` y los componentes
simplemente se tienen que importar de las otras carpetas, lo cual es bastante
simple. Aunque por ahora es bastante similar a escribir `html` usando un
framework, me gustaría que simplemente tomara un markdown como entrada, aunque
será ir paso por paso. El tutorial primero indica que hay que subirlo online,
entiendo que es un tutorial enfocado a nuevas personas, pero como en mi caso
lo quiero subir a GitHub Pages, tendré que alejarme un poco del tutorial.

Bueno, de hecho hacer que GitHub procese la página fue mucho más simple de
lo que pensé. Simplemente hay que agregar las instrucciones en el archivo
`.github/workflows/deploy.yaml`. Por ahora estoy usando las instrucciones que
se ofrece en el [tutorial de Astro](https://docs.astro.build/en/guides/deploy/github/)
por lo que fue bastante simple. Supongo que si requiero un proceso más
avanzado la cosa cambiará, pero por ahora funciona y es todo lo que pido.
Con esto, puedo continuar con el tutorial para crear un blog.

Bueno, han pasado unas cuantas horas leyendo el tutorial y la documentación.
Y he aprendido una cosa, esto es HTML con pasos extra. Permite organizar las
cosas bastante bien con los componentes, pero para nada es para crear un blog.
Esto no implica que no puedas, para nada, sino que no es su único objetivo.
Astro es un sistema bastante avanzado para poder crear páginas estáticas, es
similar a React, pero no tan enfocado a JavaScript, sino enfocado más a HTML.

La cuestión es que mi propósito al utilizar un generador de páginas estáticas
no es tanto tener un blog completamente atractivo. Sino tener un blog
funcional donde pueda enfocarme a solo escribir las entradas sin pelearme
tanto en el funcionamiento interno de la página ¿Voy a cambiar astro? Para
nada, astro es bastante interesante y siento que puedo crear cosas muy
interesantes con todas las herramientas que dan. Pero al mismo tiempo
necesito algo que me simplifique la vida.

Con este objetivo, buscando (y preguntando a ChatGPT si soy sincero) me
encontré con [Astro Themes](https://astro.build/themes/). En esta página se
pueden encontrar muchas platillas para usar. Algunas son de paga, pero otras
son gratuitas. En mi caso, después de buscar arduamente por la primera página
de resultados, me decidí por el tema [multiterm-astro](https://github.com/stelcodes/multiterm-astro)
que hace que el blog se vea como una consola de comandos.

La instalación fue sencilla, simplemente hacer un fork y usar la estructura
ya establecida. Aun hay cosas que quiero modificar, como la fuente cuando se
renderiza código. Sin embargo, para una aventura que me tomo todo un día, creo
que es suficiente.
