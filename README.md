# SASS
Une initiation au préprocesseur SASS 
Note perso : les em pour les polices et les rem pour le padding 
# Index 
## Initiation (importer)
## Imbrication 
## Héritage 
## Variables 
## Mixins et les fonctions 
## Les conditions 
## Les boucles et les listes 


# Initiation 
**Importation**
```
@import "url_relative au fichier scss"; 
``` 
# Imbrication 
**Imbrication des balises**
```
table{
    //some css code 
    td{
        //some css code
    }
}
``` 
**Imbrication et pseudo-sélecteur**
```
.btn{
    //some css code 
    &:hover{
        //some css code 
    }
}
```

**Imbrication des propriétés** 
```
selector{
    //some css code 
    background{
        color : #....; 
        repeat : no-repeat; 
    }
}
```
# Héritage 
Remarque générale : très pratique mais alourdit assez vite le code (donc faire attention) 
**Héritage basique**
```
.btn{
    //code CSS 
} 
.btn-urgent{
    @extend .btn; 
    //some individual css 
}
```
**Sélecteur générique**
```
%btn{
    //some css , NB this selector won't be compiled 
}
.btn{
    @extend %btn; 
    //some individual css 
}
```
```
%shadow{
    box-shadow : 0px 1px 5px color; 
}

selector 
{
    @extend %shadow; 
}
```

# Les variables 
Les variables SASS permettent plus de choses que les variables css 

**Déclarer une variable** 
```
$color_main : #XXXXXX; 
$padding : 20px; 
```
**Déclarer une variable-suite**
```
$variable_name : value!default; //default value i.e if not previously affected 
```
**Utiliser une variable**
```
selector{
    padding : $padding + 20px; 
}
```
**Un sélecteur variable** 
```
$medium_px : 768px; 
$medium-up : 'only screen and(min-width : #{medium_px})'; 

@media #{$medium-up}{
    //some css code 
}
```
**Quelques fonctions utiles**
Evidemment je vais remplir cette section au fur et à mesure de l'utilisation de SASS

Si vous avez des suggestions je suis preneur 

_darken and lighten_ : 
```
&:hover{
    background : darken($color, 10); //darkens the background color of 10% 
    //exact same use of lighten function 
}
```
_rgba_ 
```
&:hover{
    background : rgba($color, 0.5);
}
```

# Les mixins et les fonctions 

**Généralités**
On inclut les mixins dans un fichier dédié la plupart du temps 

Les mixins peuvent s'appeler entre-elles bien entendu 

**Déclarer une mixin**
```
@mixin rotate($rotation : 10deg){ //mixin qui prend un paramètre avec une valeur par défaut 
    -ms-transform : rotate($rotation); 
    -webkit-transform : rotate($rotation); 
    transform : rotate($rotation);
}
```

**Utiliser une mixin**
```
selector{
    @include rotate(60deg);
}
```
**Quelques exemples utiles**
```
@mixin transform($transform){
    -ms-transform : $transform; 
    -webkit-transform : $transform; 
    -o-transform : $transform; 
    -moz-transform : $transform; 
    transform : $transform; 
}

selector{
    @include transform(rotate(40deg));
}
```

```
@mixin triangle($triangle_size : 10px, $triangle_color){
    &::after{
        content : ''; 
        width : 0; 
        height : 0; 
        border-top : $triangle_size solid $triangle_color; 
        border-left : $triangle_size solid transparent;
        border-right : $triangle_size solid transparent;  
        position : absolute; //suppose donc que le parent a été positionné 
        bottom : $triangle_size * (-1); 
        left : calc(50% -#{$triangle_size}); 
    }
}
```

**Les fonctions**
Il est habituel de mettre toutes les fonctions dans un  fichier unique 

Créer une fonction 
```
$base-font-size : 16px!default; //on va avoir un problème dans ce cas à cause des unités 

@function strip-unit($number) {
  @if type-of($number) == 'number' and not unitless($number) {
    @return $number / ($number * 0 + 1);
  }

  @return $number;
}


@function rem($size, $base : $base-font-size){
    @return 1rem * $size / strip-unit($base); 
}

selector{
    padding : rem(5);  
}
@function rm($size, $base : $base-font-size){
    @return 1em * $size / strip-unit($base); 
}
```

# Les conditions 
logic operators 
* and 
* or 
* not (ex and not)
```
@if(lightness($color) > 50%){
    $color : new_value; 
}@else if (){

}@else{

}
```
```
@debug(lightness($color)); //affiche en console la valeur dans ce cas 
```

# Les boucles et les listes 
Ce chapitre va etre très trèèès important 

```
@for $i from 1 through 4{
    .m-#{i}{
        margin : 0 ($i * 1rem); 
    }
}
```

Les tableaux et les boucles (un exemple)
```
$animals : bear, lion, camel; 
@each $animal in $animals{
    .icon-#{$animal}{
        background : url(img/#{animal}.png);
    }
}
```

Les tableaux et les boucles (un exemple encore)
```
$categories : 
    chien #couleur, 
    chat  #couleur2, 
    poisson #couleur3; 


@each $category in $categories{
    //nth($catgeory, 1); commence à index 1 --> dans ce cas donc chien, chat, poisson (pas les couleurs) 
}

```