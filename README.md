# SASS
Une initiation au préprocesseur SASS 

# Index 
## Initiation (importer)
## Imbrication 
## Héritage 
## Variables 
## Mixins

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
**Quelques fonctionss utiles**
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
    
}
```



