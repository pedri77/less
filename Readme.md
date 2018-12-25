# Less lenguaje CSS - preprocesador

![less | CSS lenguaje](http://lesscss.org/public/img/less_logo.png)

## Instalación

### Con Node.JS

> npm install -g less
> lessc styles.less styles.css

### Con CDN

> < link rel="stylesheet/less" type="text/css" href="styles.less" />
<script src="//cdnjs.cloudflare.com/ajax/libs/less.js/3.9.0/less.min.js" ></script>

Documentación oficial: http://lesscss.org

# Variables

Las variables en less se definen con un @variable

```
@width: 10px;
@height: @width + 10px;

#header {
  width: @width;
  height: @height;
}
```

La documentación oficial sonre variables la puedes encontrar [aquí](http://lesscss.org/features/#variables-feature)

# Selector padre

Cuando queremos anidar varios elementos y hacer referencia a un elemento padre utilizamos el símbolo ```&```.

Un ejemplo de código sería el siguiente:

```
a {
  color: blue;
  &:hover {
    color: green;
  }
}
```

Que nos daría una salida en css así:

```
a {
  color: blue;
}

a:hover {
  color: green;
}
```

## Multiples selectores con ```&```

Puede aparecer más de una vez dentro de un selector. Esto permite referirse repetidamente a un selector principal sin repetir su nombre.
```
.link {
  & + & {
    color: red;
  }

  & & {
    color: green;
  }

  && {
    color: blue;
  }

  &, &ish {
    color: cyan;
  }
}
```

## Combinaciones de ```&```

```&``` también se puede utilizar para generar todas las permutaciones posibles de los selectores en una lista separada por comas:
```
p, a, ul, li {
  border-top: 2px dotted #366;
  & + & {
    border-top: 0;
  }
}
```
Daría como resultado:
```
p,
a,
ul,
li {
  border-top: 2px dotted #366;
}
p + p,
p + a,
p + ul,
p + li,
a + p,
a + a,
a + ul,
a + li,
ul + p,
ul + a,
ul + ul,
ul + li,
li + p,
li + a,
li + ul,
li + li {
  border-top: 0;
}
```
Puedes ampliar información [aquí](http://lesscss.org/features/#parent-selectors-feature)

# Mixins

Los mixins son una forma de incluir ("mezclar") un grupo de propiedades de un conjunto de reglas en otro conjunto de reglas. 

Los mixins nos ayudan a reciclar declaraciones para evitar mucho trabajo. 

Así que digamos que tenemos la siguiente clase:

```
a, #b {
  color: red;
}
.mixin-class {
  .a();
}
.mixin-id {
  #b();
}
```

Resultado:
```
.a, #b {
  color: red;
}
.mixin-class {
  color: red;
}
.mixin-id {
  color: red;
}
```

Documentación oficial: http://lesscss.org/features/#mixins-feature


# Extend

Permiten que una declaración herede estilos declarados por otra regla o placeholder. Los extend se declaran con el símbolo :extend 

```
nav ul {
  &:extend(.inline);
  background: blue;
}
```

# Merge
```
.mixin() {
  box-shadow+: inset 0 0 10px #555;
}
.myclass {
  .mixin();
  box-shadow+: 0 0 20px black;
}
```

# Nesting o anidaciones

En Css tendríamos el siguiente código:

```
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```

En Less:

```
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
```
También puedes combinar pseudo-selectores con tus mixins usando este método. Aquí está el clásico hack de clearfix, reescrito como un mixin (& representa el padre del selector actual):

```
.clearfix {
  display: block;
  zoom: 1;

  &:after {
    content: " ";
    display: block;
    font-size: 0;
    height: 0;
    clear: both;
    visibility: hidden;
  }
}
```
## Importación

```
@import "library"; // library.less
@import "typo.css";
```
