[]{#markdown-mermaid aria-hidden="true" dark-mode-theme="dark"
light-mode-theme="default"}

This is related to [CoderDost Course on Advance
JavaScript](https://www.youtube.com/watch?v=gUUCmRJjVvo)

# 1. Scope and Closure {#1-scope-and-closure}

-   We have 3 types of variable in JavaScript ***var***, ***let*** and
    ***const***

-   ☠️☠️ *var* is the old one, and should not be used now in any case.
    As it has many issues with creating scopes

    -   why it is still there ?

-   Also there are 4 kinds of scope in Javascript - *Block Scope*,
    *Global Scope*, *Function Scope*, *Module Scope*

## Block scope & Global Scope {#block-scope--global-scope}

The **scope** is the current context of execution in which *values* and
expressions are \"visible\"
[MDN](https://developer.mozilla.org/en-US/docs/Glossary/Scope)

**Global Scope** : Any variable/expression which is written outside -
i.e. not inside any functions, blocks etc. This is shared across files.

### let

-   this creates a *block scope*
-   *re-declaration* in NOT allowed (in same scope)
-   *re-assignment* is allowed

``` js
{ // block scope
  let x = 0;
  let y = 0;
  console.log(x); // 0
  let x = 1; // Error
}

{
  let x = 1;
  let y = 1;
  x = 2;
  console.log(x);// 2
}

console.log(x); // Error in Global Scope
```

**Temporal Dead Zone**(TDZ) : the area in which a variable is not
accessible. Temporal because it depends on time of excution not position

``` js
{
  // TDZ starts 
  const say = () => console.log(msg); // hi

  let msg = 'hi'; 
  say(); 
}
```

### const

-   this creates a *block scope*
-   *re-declaration* in NOT allowed
-   *re-assignment* is NOT allowed
-   must be assigned at declaration time.

``` js
{
  const x; //Error
  const y=0;
}

{
  const x=1;
  x=2   // Error
}

console.log(x); // Error
```

### Variable Shadowing

``` js
let x  = 0 // shadowed variable
{
  let x = 1;
  console.log(x)
}

}
```

### var

-   it doesn\'t have any block scope, and can be *re-declared*
-   it only had *function scope*
-   *var* are *hoisted*, so they can be used before the declaration

``` js
var x = 1;
var x = 2; // valid

console.log(y) // valid
var y = 3

z=4
console.log(z) // valid
var z;
```

**NOTE** : You should NOT use **var** now ❌

### let vs var

``` js
for(let i=0;i<5;i++){
  setTimeout(
    ()=>console.log(i),
    1000)
} // prints 0,1,2,3,4

for(var i=0;i<5;i++){
  setTimeout(
    ()=>console.log(i),
    1000)
} // prints 5,5,5,5,5

```

## Module scope

In modern javascript, a file can be considered as module, where we use
*export* and *import* syntax to use variable across files. We

``` html
<script src="index.js" type="module"></script>
```

``` js
export { someVar, someFunc}
```

``` js
import { someVar} from './app.js'
```

### global Object

-   The global Object is the variable **window** in case of browser.
    This helps you to use variables across the scopes. Also, it is the
    **this** value for global functions
    -   window.alert
    -   window.Promise
-   In non-browser environment, **window** doesn\'t exist. but other
    global objects exist.
-   ***var*** affects this global obejct, also ***function***
    declarations.

``` js
function sayHi(){
   console.log(this) // this will refer to window
}
```

``` js
// Strict mode can change this behaviour;
`use strict`

function sayHi(){
   console.log(window) // this is a better way of code
}
```

## function scope

-   it is created upon execution a function

``` js
function sayHi(name){
    return name;
}

sayHi() // this call will create a function scope

sayHi() // this call will create another function scope
```

#### Lexical Environment

-   Every variable in JavaScript (within global / block / or function)
    has a reference to an object-like data called *Lexical enviroment*.
    This object (kind of object) serves as the basis of search for value
    of variable.

``` js
let name = 'john'
console.log(name)
```

``` {style="all:unset;"}
Lexical Enviroment (Global variable)#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .error-icon{fill:#552222;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .error-text{fill:#552222;stroke:#552222;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edge-thickness-normal{stroke-width:2px;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edge-thickness-thick{stroke-width:3.5px;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edge-pattern-solid{stroke-dasharray:0;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .marker{fill:#333333;stroke:#333333;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .marker.cross{stroke:#333333;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a g.classGroup text .title{font-weight:bolder;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .nodeLabel,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edgeLabel{color:#131300;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edgeLabel .label rect{fill:#ECECFF;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .label text{fill:#131300;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edgeLabel .label span{background:#ECECFF;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .classTitle{font-weight:bolder;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .node rect,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .node circle,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .node ellipse,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .node polygon,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .divider{stroke:#9370DB;stroke:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a g.clickable{cursor:pointer;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .dashed-line{stroke-dasharray:3;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .dotted-line{stroke-dasharray:1 2;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #compositionStart,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #compositionEnd,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #dependencyStart,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #dependencyStart,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #extensionStart,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #extensionEnd,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #aggregationStart,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #aggregationEnd,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #lollipopStart,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a #lollipopEnd,#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .edgeTerminals{font-size:11px;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-8a31b143-e0fd-46b0-8e8a-02e3ac06533a :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[outer]nullLexicalEnviromentname: 'john'nameLexical Enviroment (Global variable)
```

``` js
let name = 'john';

function sayHi(){
  let greet = "hi"
  console.log(greet)
}

sayHi()
console.log(name, sayHi)
```

``` {style="all:unset;"}
Lexical Enviroment (functions)#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .error-icon{fill:#552222;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .error-text{fill:#552222;stroke:#552222;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edge-thickness-normal{stroke-width:2px;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .marker{fill:#333333;stroke:#333333;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .marker.cross{stroke:#333333;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 g.classGroup text .title{font-weight:bolder;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .nodeLabel,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edgeLabel{color:#131300;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .label text{fill:#131300;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edgeLabel .label span{background:#ECECFF;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .classTitle{font-weight:bolder;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .node rect,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .node circle,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .node ellipse,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .node polygon,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .divider{stroke:#9370DB;stroke:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 g.clickable{cursor:pointer;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .dashed-line{stroke-dasharray:3;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .dotted-line{stroke-dasharray:1 2;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #compositionStart,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #compositionEnd,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #dependencyStart,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #dependencyStart,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #extensionStart,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #extensionEnd,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #aggregationStart,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #aggregationEnd,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #lollipopStart,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 #lollipopEnd,#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .edgeTerminals{font-size:11px;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-1c79d9f2-3cd7-4fac-8a3a-56a77a126138 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[outer][outer]nullLexicalEnviroment1name: 'john',sayHi: functionLexicalEnviroment2greet: 'hi'namesayHigreetLexical Enviroment (functions)
```

``` js
let name = 'john';

function sayHi(){
  let greet = "hi"
  console.log(name)
}

sayHi()
```

``` {style="all:unset;"}
Lexical Enviroment (functions)#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .error-icon{fill:#552222;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .error-text{fill:#552222;stroke:#552222;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edge-thickness-normal{stroke-width:2px;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .marker{fill:#333333;stroke:#333333;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .marker.cross{stroke:#333333;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 g.classGroup text .title{font-weight:bolder;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .nodeLabel,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edgeLabel{color:#131300;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .label text{fill:#131300;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edgeLabel .label span{background:#ECECFF;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .classTitle{font-weight:bolder;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .node rect,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .node circle,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .node ellipse,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .node polygon,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .divider{stroke:#9370DB;stroke:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 g.clickable{cursor:pointer;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .dashed-line{stroke-dasharray:3;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .dotted-line{stroke-dasharray:1 2;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #compositionStart,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #compositionEnd,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #dependencyStart,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #dependencyStart,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #extensionStart,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #extensionEnd,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #aggregationStart,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #aggregationEnd,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #lollipopStart,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 #lollipopEnd,#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .edgeTerminals{font-size:11px;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-7c195620-504e-4d80-a023-3b45cf04ae31 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[outer][outer]nullLexicalEnviroment1name: 'john',sayHi: functionLexicalEnviroment2greet: 'hi'nameLexical Enviroment (functions)
```

## Hoisting

The movement of *variable declaration* to top of scope - before
execution

-   *function declarations* are properly hoisted (value accessible)
-   *var* is hoisted.

``` js
let name = 'john';

sayHi() // valid

function sayHi(){
  let greet = "hi"
  console.log(name)
}

sayHello() // error
let sayHello = function(){
   console.log(name)
}
```

**Temporal Dead Zone**(TDZ) :

``` js
let x = 1;

{
  console.log(x) // Reference error
  let x = 2; 
}
```

## Closures

-   we can create nested functions in JavaScript

``` js
function createUser(name){
  let greeting = 'Hi ' 
  function greet(){
     return greeting + name + ' is Created';
  }
  return greet()
}

createUser('john') // Hi john is created;
```

-   Now more useful work is if we can return the `greet` function
    itself.

``` js
function createUser(name){
  let greeting = 'Hi ' 
  function greet(){
     return greeting + name + ' is Created';
  }
  return greet // returned just definition of function
}

let welcomeJohn = createUser('john') 
welcomeJohn() // // Hi john is created;
```

-   This is **Closure**
    -   *welcomeJohn* function definition has access
        -   to outer **params** ( *name* ) which came for *createUser*
            function
        -   also any other \"variables\" declared inside *createUser*
            will also be accessible to this *welcomeJohn*

### Example

``` js
function initCounter() {
  let count = 0;
  return function () {
    count++;
  };
}

let counter = initCounter();
counter() // 0
counter() // 1

let counter1 = initCounter();
counter1() // 0
counter1() // 1
```

**NOTE** : so whenever you have a function which wants to preserve a
value over many calls - it\'s a time for closure.

#### Lexical Environment

``` js
function init() {
  let name = 'john';

  function greet() {
    console.log(name)
  }
  return greet;
}

let sayHi = init();

sayHi();
```

``` {style="all:unset;"}
Lexical Enviroment (functions)#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .error-icon{fill:#552222;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .error-text{fill:#552222;stroke:#552222;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edge-thickness-normal{stroke-width:2px;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .marker{fill:#333333;stroke:#333333;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .marker.cross{stroke:#333333;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 g.classGroup text .title{font-weight:bolder;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .nodeLabel,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edgeLabel{color:#131300;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .label text{fill:#131300;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edgeLabel .label span{background:#ECECFF;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .classTitle{font-weight:bolder;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .node rect,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .node circle,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .node ellipse,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .node polygon,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .divider{stroke:#9370DB;stroke:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 g.clickable{cursor:pointer;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .dashed-line{stroke-dasharray:3;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .dotted-line{stroke-dasharray:1 2;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #compositionStart,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #compositionEnd,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #dependencyStart,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #dependencyStart,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #extensionStart,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #extensionEnd,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #aggregationStart,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #aggregationEnd,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #lollipopStart,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 #lollipopEnd,#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .edgeTerminals{font-size:11px;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-cdaf6096-8861-4b93-854d-caf620f744f0 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[outer][outer][outer]nullLexicalEnviroment1sayHi: ----init: functionLexicalEnviroment2name: 'john'greet: functionLexicalEnviroment3--empty--initnamesayHiLexical Enviroment (functions)
```

### Real life example 1

``` js
function initCounter(id) {
  let count = 0;
  return function () {
    count++;
    document.getElementById(id).innerText = count;
  };
}
let count = 10;
let counter1 = initCounter('btnCount1');
let counter2 = initCounter('btnCount2');

// here `btn1` and `btn2` are id of HTML buttons.
  
```

``` html
<button onclick="counter1()">1</button>
<p id="btnCount1"></p>
<button onclick="counter2()">2</button>
<p id="btnCount2"></p>
```

### Real life example 2

``` js
function initAddString(inputId, outputId) {
  let str = '';
  return function () {
    str += ' ' + document.getElementById(inputId).value;
    document.getElementById(inputId).value = '';
    document.getElementById(outputId).innerText = str;
  };
}

let strAdder1 = initAddString('text1', 'text-output1');
let strAdder2 = initAddString('text2', 'text-output2');
```

``` html
<input type="text" id="text1">
<button onclick="strAdder1()">Add String</button>
<p id="text-output1"></p>

<input type="text" id="text2">
<button onclick="strAdder2()">Add String</button>
<p id="text-output2"></p>
```

## IIFE - Immediately Invoked Function Expression

-   this practice was popular due to *var*.
-   Immediately invoking a function avoids - re-declaration of variables
    inside it

``` js
// Immediately invoked function expressions
(function(){
      var x = 1;   // this var is now protected
})()


(function(a){
      var x = a;   // this var is now protected
})(2)
```

## Currying

``` js
function sum(a){
  return function(b){
    return function(c){
       console.log(a,b,c)
       return a+b+c
    }
  }
}

let add = a => b => c => a+b+c

let log = time => type => msg => `At ${time.toLocaleString()}: severity ${type} => ${msg}`

log(new Date())('error')('power not sufficient')

let logNow = log(new Date())

logNow('warning')('temp high')

let logErrorNow = log(new Date())('error')

logErrorNow('unknown error')
```

``` js
function op(operation) {
  return function (a) {
    return function (b) {
      return operation === 'add' ? a + b : a - b;
    };
  };
}

const add3 = op('add')(3);
const sub3 = op('sub')(3);
const add = op('add');

add3(6);
sub3(6);
add(1)(2);
```

------------------------------------------------------------------------

# 2. Objects {#2-objects}

## Basic behaviours

### Reference Copying

-   Variable value is not copied in case of object/arrays

``` js
let person =  {name:'john'}
let human = person;
```

``` {style="all:unset;"}
Reference are point to same value#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .error-icon{fill:#552222;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .error-text{fill:#552222;stroke:#552222;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .edge-thickness-normal{stroke-width:2px;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .marker{fill:#333333;stroke:#333333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .marker.cross{stroke:#333333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .cluster-label text{fill:#333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .cluster-label span,#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 p{color:#333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .label text,#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 span,#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 p{fill:#333;color:#333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .node rect,#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .node circle,#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .node ellipse,#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .node polygon,#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .flowchart-label text{text-anchor:middle;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .node .label{text-align:center;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .node.clickable{cursor:pointer;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .arrowheadPath{fill:#333333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .flowchart-link{stroke:#333333;fill:none;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .cluster text{fill:#333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .cluster span,#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 p{color:#333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-041dd1e1-2029-4f6e-aeac-880e027763c5 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}personObjecthumanReference are point to same value
```

``` js
let person =  {name:'john'} // Object1
person = {name:'wick'}; // Object2
```

``` {style="all:unset;"}
Reference can be changed for a variable (Garbage collection of Object1)#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .error-icon{fill:#552222;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .error-text{fill:#552222;stroke:#552222;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .edge-thickness-normal{stroke-width:2px;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .marker{fill:#333333;stroke:#333333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .marker.cross{stroke:#333333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .cluster-label text{fill:#333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .cluster-label span,#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 p{color:#333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .label text,#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 span,#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 p{fill:#333;color:#333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .node rect,#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .node circle,#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .node ellipse,#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .node polygon,#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .flowchart-label text{text-anchor:middle;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .node .label{text-align:center;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .node.clickable{cursor:pointer;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .arrowheadPath{fill:#333333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .flowchart-link{stroke:#333333;fill:none;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .cluster text{fill:#333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .cluster span,#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 p{color:#333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-b6e55a0b-f0bb-4f70-b3aa-68397f80b8b4 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}personObject1Object2Reference can be changed for a variable (Garbage collection of Object1)
```

-   it a better to use *const* always, and whenever you must need to
    re-assign change it ot *let*

``` js
const person  = {name:'john'} // Object1
person = {name:'wick'}; // ERROR 
```

### Nested Objects

``` js
let person = {
  name: 'John',
  address: { city: 'delhi', state: 'delhi' },
};
```

``` {style="all:unset;"}
Object properties can point to other objects#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .error-icon{fill:#552222;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .error-text{fill:#552222;stroke:#552222;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .edge-thickness-normal{stroke-width:2px;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .marker{fill:#333333;stroke:#333333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .marker.cross{stroke:#333333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .cluster-label text{fill:#333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .cluster-label span,#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 p{color:#333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .label text,#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 span,#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 p{fill:#333;color:#333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .node rect,#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .node circle,#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .node ellipse,#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .node polygon,#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .flowchart-label text{text-anchor:middle;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .node .label{text-align:center;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .node.clickable{cursor:pointer;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .arrowheadPath{fill:#333333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .flowchart-link{stroke:#333333;fill:none;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .cluster text{fill:#333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .cluster span,#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 p{color:#333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-c40eeb5a-d09e-4c46-aa62-9b469db6fba3 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}personObjectObject_addressaddressObjectObject properties can point to other objects
```

``` js
let addressObject = { city: 'delhi', state: 'delhi' }

let person = {
  name: 'John',
  address: addressObject
};
```

### Copying objects

#### Shallow Copy

Many methods can be used to *copy* object without old reference

1.  **Object.assign()**

``` js
let person =  {name:'john'}
let newPerson = Object.assign({}, person) 
```

2.  **Spread Operator\[\...\]**

``` js
let person =  {name:'john'}
let newPerson = {...person} 
```

But problem which these is they just create a copy of *properties* of
that object , but not creating a copy of their references also.

``` js
let addressObject = { city: 'delhi', state: 'delhi' }

let person = {
  name: 'John',
  address: addressObject
};


let newPerson = Object.assign({}, person)
person === newPerson;  // false
person.address === newPerson.address // true
```

#### Deep Copy

This is a hard problem to solve in past as there can be multiple level
of nested objects and there can be references to functions etc also. few
methods which are there:

1.  **JSON.stringify and JSON.parse** : this method utilizes the fact
    that every JSON can be converted to a string value (exception of
    methods/functions)

``` js
let addressObject = { city: 'delhi', state: 'delhi' }

let person = {
  name: 'John',
  address: addressObject
};

let str = JSON.stringify(person)
let jsonObject = JSON.parse(str);
```

2.  **structuredClone** : Browser API which work even for circular
    references (but functions not supported)

``` js
let addressObject = { city: 'delhi', state: 'delhi' }

let person = {
  name: 'John',
  address: addressObject,
};

person.me = person

let newPerson = structuredClone(person);
```

### \"this\" and Methods

-   we can also defined *function* as value to properties of objecy.
    these will be called *methods*. Methods are just functions but, it
    means they have been called in \"reference\" on an Object.

``` js
let person =  {
  name:'john',
  sayHi: function(){
    return "hi";
  }
} 

person.sayHi() // hi
```

-   methods can also access the *properties* and other *methods* of same
    object. To do this we use *this*

``` js
let person =  {
  name:'john',
  sayHi: function(){
    return "hi "+ this.name;
  }
} 

person.sayHi() // hi john
```

-   we can also have used *person* instead of *this* but has you know
    references can be changed. so that could have created a problem

``` js
let person =  {
  name:'john',
  sayHi: function(){
    return "hi "+ this.name;
  }
} 

person.sayHi() // hi john
```

-   you can even have *this* without an object

``` js
function sayHi(){
    return "hi "+ this.name; 
}
sayHi() // Error
// here this will "undefined" in Strict mode
let obj1 = {name: 'john'}
let obj2 = {name: 'wick'}

// you can add functional property

obj1.say = sayHi;
obj2.say = sayHi;


obj1.say() //  hi john
obj2.say() //  hi wick 
```

-   Arrow functions don\'t have a *this*. they use outer context

``` js
let person =  {
  name:'john',
  sayHi: ()=> {
    return "hi "+ this.name;
  }
} 

person.sayHi() // Error
```

## Symbol

-   JavaScript also has a *Symbol* data type. This data type is used as
    *property* name in Objects.
-   Object can only have 2 types of *properties* - String and Symbol. If
    you put any other data type they will convert to String

``` js
let person =  {
  0:'john',
  sayHi: ()=> {
    return "hi "+ this.name;
  }
} 

person["0"] // this number will convert to string
```

-   *Symbol* is used for making hidden (library used properties)

``` js
const id = Symbol("id"); // "id" is descriptor

let person =  {
  name:'john',
  [id]:1
} 

person[id] // 1

// note that we have put square [] on property so that it is not confused with "id" string.
```

-   *Symbol* are always unique - so there is no chance of collision.
    Even with same \"descriptor\" they will be uniquely initialized.

-   You can get *Symbol* for some descriptor or key using some methods

``` js
// get symbol by name 
let sym = Symbol.for("name"); 
let sym2 = Symbol.for("id");
```

*for..in* loop ignore Symbols. Also methods like *Object.keys()* ignore
these properties.

------------------------------------------------------------------------

# 3. Functions {#3-functions}

## functions are objects

-   they already have some predefined properties *name*, *length* etc
-   you can also make more properties on functions (but generally it\'s
    not required, except for Constructor function)

``` js
function sayHi(greet){
   return greet
}
sayHi.name // name of function
sayHi.length // length of arguments

sayHi.count =0; // function can have properties
sayHi.count++;
sayHi.count;
```

## function declaration are hoisted

``` js
sayHi() // works
function sayHi(greet){
   return greet
}

sayHello() // Error
let sayHello = function(){ // functional expression
  
}

sayHello.name // sayHello
```

## function can be called as constructor

``` js
function Person(name){
    this.name = name
}

const p = new Person('john') // constructor 
```

## Named function expression (NFE)

``` js
let sayHello = function fx(user){ // named functional expression

   if(user){
      return "hello " + user
   } else {
      return fx('anonymous')
   }
}

// this can help in case where sayHello is re-assiged to something

let sayHi = sayHello
sayHello = null
sayHi()
```

## Decorator (Wrappers)

-   It\'s a *design pattern* in which you modify the functionality of a
    function by covering it inside a wrapper.

``` js
let modifiedFx = Decorator(preDefinedFx)
```

### Memoization (Caching)

``` js
function heavy(x) {
  console.log(x + ':heavy');
  return x + ':heavy';
}

function memoized(fx) {
  let map = new Map();
  
  return function (x) {  // wrapper
    if (map.has(x)) {
      return map.get(x);
    } else {
      let memoValue = fx(x);
      map.set(x, memoValue);
      return memoValue;
    }
  };
}

let memoizedHeavy = memoized(heavy)
memoizedHeavy(2);
memoizedHeavy(2); // take from cache
```

**Another Problem**

-   if you try to use this on a *method* of object, this approach can
    fail

``` js
let task = {
  name: 'demo',
  heavy(x) {
    console.log(x + ':heavy:' + this.name);
    return x + ':heavy' + this.name;
  },
};

function memoized(fx) {
  let map = new Map();
  return function (x) {
    if (map.has(x)) {
      return map.get(x);
    } else {
      let memoValue = fx(x);
      map.set(x, memoValue);
      return memoValue;
    }
  };
}
task.memoizedHeavy = memoized(task.heavy) 
task.memoizedHeavy(1) // 1:heavyundefined
```

**Solution** : use *function.call()*

### changing \'this\'

###### Call

``` js
person = {
  name: 'demo',
  age: 12,
  location: 'delhi',
};

function checkName(a) {
  return !!this.name;
}

checkName() // Error 
checkName.call(person)
checkName.call(person, 1) // a = 1
```

###### apply

``` js
person = {
  name: 'demo',
  age: 12,
  location: 'delhi',
};

function checkName(a) {
  return !!this.name;
}

checkName() // Error 
checkName.apply(person)
checkName.apply(person, [1]) // a = 1
```

###### bind

``` js
person = {
  name: 'demo',
  age: 12,
  location: 'delhi',
};

function checkName(a) {
  return !!this.name;
}

checkName() // Error 
let boundCheckName = checkName.bind(person)
boundCheckName();
```

**Solution**

``` js
let task = {
  name: 'demo',
  heavy(x) {
    console.log(x + ':heavy:' + this.name);
    return x + ':heavy' + this.name;
  },
};

function memoized(fx) {
  let map = new Map();
  return function (x) {
    if (map.has(x)) {
      return map.get(x);
    } else {
      let memoValue = fx.call(this,x);
      map.set(x, memoValue);
      return memoValue;
    }
  };
}
task.memoizedHeavy = memoized(task.heavy) 
task.memoizedHeavy(1) // 1:heavydemo
```

### Debounce

-   Run a function only when - if it has not been called again for a
    fixed *period*
-   Suppose you are typing and take a pause of 1 second. Only then that
    function should be called.

``` js
let count = 1;
function showCount() {
  count++;
  console.log({ count });
}

function debounce(fx, time) {
  let id = null;
  return function (x) {
    if (id) {
      clearTimeout(id);
    }
    console.log({ id });
    id = setTimeout(() => {
      fx(x);
      id = null;
    }, time);
  };
}

let showCountD = debounce(showCount, 2000);
setTimeout(showCountD, 1000);
setTimeout(showCountD, 1500);
setTimeout(showCountD, 2000);
setTimeout(showCountD, 2500);
setTimeout(showCountD, 5000);
```

##### Real Example

``` js
const el = document.getElementById('text1');
const logo = document.getElementById('text-output1');
el.addEventListener(
  'keyup',
  debounce(function (e) {
    logo.innerText = e.target.value;
  }, 1000)
);
```

``` html
<input type="text" id="text1">
<p id="text-output1"></p>
```

#### Throttle

-   when you have to only allow 1 execution of a function within a
    *period* of time
-   for example you are *scrolling* fast but only 1 scroll per 100
    millisecond is considered.

``` js
let count = 1;
function showCount() {
  count++;
  console.log({ count });
}

function throttle(fx, time) {
  let id = null;
  let arg = [];
  return function (x) {
    arg[0] = x;
    if (!id) {
      id = setTimeout(() => {
        fx(arg[0]);
        id = null;
      }, time);
    }
    console.log({ id });
  };
}

let showCountT = throttle(showCount, 2000);
setTimeout(showCountT, 1000);
setTimeout(showCountT, 1500);
setTimeout(showCountT, 2000);
setTimeout(showCountT, 2500);
setTimeout(showCountT, 5000);
```

##### Real Example

``` js
function throttle(fx, time) {
  let id = null;
  let arg = [];
  return function (x) {
    arg[0] = x;
    if (!id) {
      id = setTimeout(() => {
        fx(arg[0]);
        id = null;
      }, time);
    }
  };
}

function sayHi(){console.log('hi')}
document.addEventListener('scroll',throttle(sayHi,1000))
```

## Arrow functions

#### Differences

-   they don\'t have *this*
-   they don\'t have *arguments*,
-   they can\'t be called with *new* (as constructor)

#### Similarities

-   they have properties like *name*, *length*

------------------------------------------------------------------------

# 4. Iterables, Generators {#4-iterables-generators}

## Iterables and Iterators

### Iterable (protocol)

-   *Iterables* are objects in which we can make array like iteration
    (Example using *for..of* loop of *spread operators*)

    -   Array are *iterables*
    -   String are *iterables*

-   To make any object iterable we have these conditions

    -   implement a *Symbol.iterator* property, which should be a
        function which return an *Iterator* Object

``` js
iterable[Symbol.iterator]() => Iterator
```

### Iterator (protocol)

Iterators are objects which have :

-   a *next()* method which return a object which is of format
    `{value:-some-value-, done:-boolean-}` e.g. \*{value: 1, done:
    false}
-   **value** is the value we are interested in, while **done** tells us
    when to stop. Generally when *done:true* the *value:undefined*

Now, making an Iterable is like this:

``` js
let iterator = {
  i: 0,
  next: function () {
    return { value: this.i, done: this.i++ > 5 };
  },
};

let iterable = {
  name: 'john',
  age: 34,
  [Symbol.iterator]() {
    return iterator;
  },
};
```

#### Example - Range : {#example---range-}

``` js
let range = {
  start: 0,
  end: 5,
  [Symbol.iterator]() {
    let that = this; // this line is very important
    let i = this.start;
    return { // iterator object
      next: function () {
        return { value: i, done: i++ > that.end };
      }
    };
  },
};
```

#### Array

``` js
let num = [1, 2, 3];
let iterator = num[Symbol.iterator]();
iterator.next();
iterator.next();
iterator.next();
iterator.next();
```

## Infinite iterators

-   As we can see that we can control, how to control the *next()*
    function. In few cases, it will be useful to have *iterators* which
    can need to generate the next value infinitely
-   If you use such *iterators* in a loop etc. it can be dangerous as
    can create infinite loop. But can be controlled by `break` etc.
-   we will cover all this in generators.

## Iterables vs Array-like

-   *Iterable* objects are based on *Symbol.iterator* method as defined
    above
-   *Array-like* objects are based on array protocols (index and length)

An object can be

-   *Iterable* + *Array-like*
-   *Iterable* only
-   *Array-like* only
-   None of them (not *Iterable* nor *Array-like* )

**Example** :

``` js
// iterable + array-like
let arr = [1,2,3] 


// only iterable
let range = {
  start: 0,
  end: 5,
  [Symbol.iterator]() {
    let that = this; // this line is very important
    let i = this.start;
    return {
      next: function () {
        return { value: i, done: i++ > that.end };
      },
    };
  },
};

// only array-like
let array = {
  0: 1,
  1: 5,
  length:2
};


// none
let obj = {
 name:'john'
}
```

### Conversions

#### Array-like to Array

-   **Array.from()** : method is used for this

``` js
let arrayLike = {
  0: 0,
  1: 5,
  length: 2
};

let arr = Array.from(arrayLike);

// also used for general things

let set = new Set()
set.add(1);
set.add(2);
let arr2 = Array.from(set) // [1,2]
```

## Map

-   this data type is also *iterable*
-   special this is can have keys also as *numbers*, *booleans*,
    *objects*
-   also map maintains the *order* of keys added.

``` js
let map = new Map();


let person = {name:'john'}
let personAccount = {balance: 5000}

map.set('1', 'str1');   //  string key
map.set(1, 'num1');     //  numeric key
map.set(true, 'bool1'); 
map.set (person, personAccount)

map.get(1)  // 'num1'
map.get('1') // 'str1'
map.get(person) // { balance : 5000 }

map.size // 4

map.keys() // iterable of keys
map.values() // iterable of values
map.entries() // iterable of key-value pair

map.has(1) // key exists
```

#### Converting Object to Map

-   We can use **Object.entries()** method for this.

``` js
let obj = {a:1,b:2,c:3};
let map = new Map(Object.entries(obj));
```

#### Converting Map to Object

-   We can use **Object.fromEntries()** method for this.

``` js
let map = new Map();
map.set('a', 1);
map.set('b', 2);
map.set('c', 3);

let obj = (Object.fromEntries(map.entries())); // {a:1,b:2,c:3}
```

## Set

-   Set is another *iterable*
-   Set only contains uniques elements

``` js
let set = new Set();

let obj1 = { name: "John" };
let obj2 = { name: "Jack" };
let obj3 = { name: "Peter" };

set.add(obj1);
set.add(obj2);
set.add(obj3);
set.add(obj2);
set.add(obj3);

// set keeps only unique values
set.size; // 3

set.keys() // iterable of keys
set.values() // iterable of values (Same as keys)
set.entries()
```

-   duplicated values in *values()*, *entries()* etc are maintained to
    match *Map* compatibility

## WeakMap and Weakset

-   These are 2 alternative way of creating *Map* or *Set* like data
    types - when only object keys are considered.
-   They have very limited operations and doesn\'t support all
    functionality
-   Main purpose is that when *keys* are marked as *null* they are
    garbage collected. So this helps in better memory management

``` js
let weakMap = new WeakMap()
let person = {name:'john'}

weakMap.set(person, {....});

person = null // in future we decide to remove this key

// so weakMap will remove it from memory space automatically
```

## Generators

-   Easy way to create an *iterators* and *iterables*

``` js
function* generatorFunction(){
 yield 1;
 yield 2;
 yield 3
} 

let generator = generatorFunction();
generator.next() // {value:1, done:false}
generator.next() // {value:2, done:false}
generator.next() // {value:3, done:false}
generator.next() // {done:true}
```

#### Infinite iterator

``` js
function* generator() {
  let i = 0;
  while (true) {
    yield i;
    i++;
  }
}

const gen = generator();

function createID(it) {
  return it.next().value;
}

createID(gen);
createID(gen);
createID(gen);
createID(gen);
createID(gen);
```

#### Generator objects are \"iterables\"

``` js
function* generatorFunction(){
 yield 1;
 yield 2;
 yield 3
} 

let generator = generatorFunction();
let nums = [...generator] // [1,2,3]
```

**NOTE**: Don\'t put a *Spread operator* or *for..of* loop on inifinite
iterable

#### Range example - using generator

``` js
let range = {
  start: 0,
  end: 5,

  *[Symbol.iterator]() {  // * makes it generator function
    for(let value = this.start; value <= this.end; value++) {
      yield value;
    }
  }
};

for(let r of range){
    console.log(r)
}
```

**Better version - with function**

``` js
function range(start,end){
  return {
  *[Symbol.iterator]() { 
    for(let value = start; value <= end; value++) {
      yield value;
    }
  }
}
};

for(let r of range(1,5)){
    console.log(r)
}

let values = [...range(1,5)]
```

**Better - Better version - with function**

``` js
function* range(start,end){
  for(let value = start; value <= end; value++) {
    yield value;
  }
};


let generator = range(1,5)

console.log([...generator]) // [1,2,3,4,5]
```

### return

-   only difference it that instantly ends the iterator at that value;

``` js
function* generatorFunction(){
 yield 1;
 yield 2;
 return 3
} 

let generator = generatorFunction();
generator.next()  // {value:1, done:false}
generator.next()  // {value:2, done:false}
generator.next()  // {value:3, done:true} ** 
```

### Generator - composition

-   using *generator* inside another *generator* is easy

\*\*Composed Generator using - yield\*

``` js
function* range(start,end){
  for(let value = start; value <= end; value++) {
    yield value;
  }
};


function* multiRange(){
     yield* range(0,5),
     yield* range(100,105)
     yield* range(200,205)
}


let generator = multiRange();

console.log([...generator]) //[ 0, 1, 2, 3, 4, 5, 100, 101, 102, 103, 104, 105, 200, 201, 202, 203, 204, 205 ]
```

### Generator can also take inputs

-   **next()** method can also take arguments which act as return value
    of previous *yield* statement

``` js
function* generatorFunction(){
  let result = yield 1;
  console.log(result)
  let result2 = yield 2;
  console.log(result2)
  let result3 = yield 3
  console.log(result3)

 } 
 
let generator = generatorFunction();
let r1 = generator.next() 
let r2 = generator.next(r1.value) 
let r3 = generator.next(r2.value) 
generator.next(r3.value)
```

## Async Iterators/ Async generators

**without generators**

``` js
let range = {
  start: 0,
  end: 5,
  [Symbol.asyncIterator]() {
    let that = this; // this line is very important
    let i = this.start;
    return {
      next: async function () {
        await new Promise((resolve) => setTimeout(resolve, 1000));
        return { value: i, done: i++ > that.end };
      },
    };
  },
};

(async function () {
  for await (let f of range) {
    console.log(f);
  }
})();
```

**with generators**

``` js
let range = {
  start: 0,
  end: 5,
  async *[Symbol.asyncIterator]() {
       for(let i = this.start; i <= this.end; i++) {
       await new Promise((resolve) => setTimeout(resolve, 1000));
        yield i
       };
  },
};

(async function () {
  for await (let f of range) {
    console.log(f);
  }
})();
```

### Real-life Example - Paginated API calls

-   this example has also used *Composition* of generators

``` js
async function* getDataAsync(page) {
  let response = await fetch(
    'https://projects.propublica.org/nonprofits/api/v2/search.json?q=x&page='+page
  );
  let result = await response.json();
  for(let org of result.organizations){
    yield org.name;
  }
}


async function* getData() {
  let response = await fetch(
    'https://projects.propublica.org/nonprofits/api/v2/search.json?q=x'
  );
  let result = await response.json();
 

  for (let i = 0; i <= result.num_pages; i++) {
    yield* await getDataAsync(i);
  }
}

(async function () {
  let orgs = []
  for await (let f of getData()) {
    orgs.push(f);
  }
  console.log(orgs);  // List of all organization in API
})();
```

------------------------------------------------------------------------

# 5. ProtoTypes {#5-prototypes}

## Prototypical Inheritance

-   Objects are *extended* from other Objects. And we can re-use their
    *properties* and *methods*.
-   Object are chained in *prototypical inheritance*
-   Objects have a hidden property called `[[Prototype]]`

------------------------------------------------------------------------

``` {style="all:unset;"}
Prototype Inheritance#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .error-icon{fill:#552222;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .error-text{fill:#552222;stroke:#552222;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edge-thickness-normal{stroke-width:2px;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .marker{fill:#333333;stroke:#333333;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .marker.cross{stroke:#333333;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 g.classGroup text .title{font-weight:bolder;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .nodeLabel,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edgeLabel{color:#131300;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .label text{fill:#131300;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edgeLabel .label span{background:#ECECFF;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .classTitle{font-weight:bolder;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .node rect,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .node circle,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .node ellipse,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .node polygon,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .divider{stroke:#9370DB;stroke:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 g.clickable{cursor:pointer;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .dashed-line{stroke-dasharray:3;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .dotted-line{stroke-dasharray:1 2;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #compositionStart,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #compositionEnd,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #dependencyStart,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #dependencyStart,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #extensionStart,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #extensionEnd,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #aggregationStart,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #aggregationEnd,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #lollipopStart,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 #lollipopEnd,#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .edgeTerminals{font-size:11px;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-d78fb454-5186-4f17-82f9-7a050ad61451 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]]prototypeObjectobjectPrototype Inheritance
```

``` {style="all:unset;"}
Prototype example#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .error-icon{fill:#552222;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .error-text{fill:#552222;stroke:#552222;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edge-thickness-normal{stroke-width:2px;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edge-thickness-thick{stroke-width:3.5px;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edge-pattern-solid{stroke-dasharray:0;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .marker{fill:#333333;stroke:#333333;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .marker.cross{stroke:#333333;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae g.classGroup text .title{font-weight:bolder;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .nodeLabel,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edgeLabel{color:#131300;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edgeLabel .label rect{fill:#ECECFF;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .label text{fill:#131300;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edgeLabel .label span{background:#ECECFF;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .classTitle{font-weight:bolder;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .node rect,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .node circle,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .node ellipse,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .node polygon,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .divider{stroke:#9370DB;stroke:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae g.clickable{cursor:pointer;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .dashed-line{stroke-dasharray:3;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .dotted-line{stroke-dasharray:1 2;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #compositionStart,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #compositionEnd,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #dependencyStart,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #dependencyStart,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #extensionStart,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #extensionEnd,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #aggregationStart,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #aggregationEnd,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #lollipopStart,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae #lollipopEnd,#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .edgeTerminals{font-size:11px;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-15bd5307-85fd-4270-aaa2-3fbdc0e256ae :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]]animaleatsdogbarksanimal is prototype of dogdog is 
prototypically inherited 
from animalPrototype example
```

``` js
let animal = { eats: true }; 
let dog = { barks: true };
dog.__proto__ = animal; 

dog.barks // true
dog.eats // true
```

``` {style="all:unset;"}
Prototype chaining#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .error-icon{fill:#552222;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .error-text{fill:#552222;stroke:#552222;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edge-thickness-normal{stroke-width:2px;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .marker{fill:#333333;stroke:#333333;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .marker.cross{stroke:#333333;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 g.classGroup text .title{font-weight:bolder;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .nodeLabel,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edgeLabel{color:#131300;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .label text{fill:#131300;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edgeLabel .label span{background:#ECECFF;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .classTitle{font-weight:bolder;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .node rect,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .node circle,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .node ellipse,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .node polygon,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .divider{stroke:#9370DB;stroke:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 g.clickable{cursor:pointer;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .dashed-line{stroke-dasharray:3;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .dotted-line{stroke-dasharray:1 2;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #compositionStart,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #compositionEnd,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #dependencyStart,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #dependencyStart,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #extensionStart,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #extensionEnd,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #aggregationStart,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #aggregationEnd,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #lollipopStart,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 #lollipopEnd,#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .edgeTerminals{font-size:11px;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-fbae530d-a259-4f09-9d07-f4d0aaf686b1 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]]animaleatswalks()dogbarksPrototype chaining
```

``` js
let animal = {
  eats: true,
  walks: function () {
    return 'walks';
  },
};
let dog = { barks: true };


dog.__proto__ = animal; 

dog.walks() // walks
```

``` {style="all:unset;"}
Prototype chain can be longer and longer#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .error-icon{fill:#552222;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .error-text{fill:#552222;stroke:#552222;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edge-thickness-normal{stroke-width:2px;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edge-thickness-thick{stroke-width:3.5px;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edge-pattern-solid{stroke-dasharray:0;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .marker{fill:#333333;stroke:#333333;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .marker.cross{stroke:#333333;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe g.classGroup text .title{font-weight:bolder;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .nodeLabel,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edgeLabel{color:#131300;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edgeLabel .label rect{fill:#ECECFF;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .label text{fill:#131300;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edgeLabel .label span{background:#ECECFF;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .classTitle{font-weight:bolder;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .node rect,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .node circle,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .node ellipse,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .node polygon,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .divider{stroke:#9370DB;stroke:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe g.clickable{cursor:pointer;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .dashed-line{stroke-dasharray:3;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .dotted-line{stroke-dasharray:1 2;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #compositionStart,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #compositionEnd,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #dependencyStart,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #dependencyStart,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #extensionStart,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #extensionEnd,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #aggregationStart,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #aggregationEnd,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #lollipopStart,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe #lollipopEnd,#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .edgeTerminals{font-size:11px;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-82e9f11e-06c3-4051-b9c0-bd7db8aaefbe :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]][[prototype]]animaleatswalks()dogbarksmyDognamePrototype chain can be longer and longer
```

``` js
let animal = {
  eats: true,
  walks: function () {
    return 'walks';
  },
};
let dog = { barks: true };
let myDog = { name: 'sifu' };


dog.__proto__ = animal; 
myDog.__proto__ = dog; 

myDog.name // sifu
myDog.barks  // true
myDog.walks() // walks
```

``` {style="all:unset;"}
Prototype end at "null"#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .error-icon{fill:#552222;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .error-text{fill:#552222;stroke:#552222;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edge-thickness-normal{stroke-width:2px;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .marker{fill:#333333;stroke:#333333;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .marker.cross{stroke:#333333;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 g.classGroup text .title{font-weight:bolder;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .nodeLabel,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edgeLabel{color:#131300;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .label text{fill:#131300;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edgeLabel .label span{background:#ECECFF;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .classTitle{font-weight:bolder;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .node rect,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .node circle,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .node ellipse,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .node polygon,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .divider{stroke:#9370DB;stroke:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 g.clickable{cursor:pointer;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .dashed-line{stroke-dasharray:3;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .dotted-line{stroke-dasharray:1 2;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #compositionStart,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #compositionEnd,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #dependencyStart,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #dependencyStart,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #extensionStart,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #extensionEnd,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #aggregationStart,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #aggregationEnd,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #lollipopStart,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 #lollipopEnd,#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .edgeTerminals{font-size:11px;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-52d00071-5af8-4d0a-b5ca-9c2d6d635d72 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]][[prototype]]nullObject_prototypeanimaleatswalks()dogbarksmyDognamePrototype end at "null"
```

## \_\_proto\_\_ {#__proto__}

-   `__proto__` is a getter/setter for `[[Prototype]]`
-   Writing property, doesn\'t call inherited properties. Except for
    `getter/setter` properties.
-   `__proto__` is not used now , and recommended way is to use
    *Object.getPrototypeOf()* and *Object.setPrototypeOf*

``` js
let animal = {
  eats: true,
  walks: function () {
    return 'walks';
  },
};
let dog = { barks: true };
let myDog = { name: 'sifu' };


dog.__proto__ = animal; 
myDog.__proto__ = dog; 

myDog.walks = function(){
   return 'walks slowly'; // this will not affect prototype
} 

myDog.walks() // walks slowly
dog.walks() // walks 
```

-   *for..in* loop works on all properties which are *enumerable* -
    *inherited* or *own*
-   if you want to `avoid` looping on inherited ones use `Object.hasOwn`
    or `Object.prototype.hasOwnProperty`
-   *Object.keys()* and *Object.value()* these will avoid `inherited`
    properties.

## .prototype property, constructor

### properties

``` js
// simple object initialization

let usr = {
   name : 'john'
}


// now using a constructor function

function User(name){
     this.name = name
}

let user = new User('john');

console.log(user) 
// User{ name :  'john'}
console.log(usr)
// {name : 'john'}
```

-   Step 1 : **.prototype** proptery is automatically created (on
    *User*) and is assigned an object (empty Object)

``` js
function User(name){
     this.name = name
}

let user = new User('john');

console.log(User.prototype) // prototype object
```

-   Step 2 :**constructor** method is assigned to this prototype, and
    that is *User* function itself.

``` js
// User.prototype.constructor = User

// this above assignment is done by the constructor call itself
User.prototype.constructor === User // true
```

-   Step 3: **.prototype** property\'s object is assigned to created
    instances.

``` js
// user.__proto__ = User.prototype
// this above assignment is done by the constructor call itself

user.__proto__ === User.prototype // true
```

``` {style="all:unset;"}
.prototype property#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .error-icon{fill:#552222;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .error-text{fill:#552222;stroke:#552222;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edge-thickness-normal{stroke-width:2px;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .marker{fill:#333333;stroke:#333333;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .marker.cross{stroke:#333333;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 g.classGroup text .title{font-weight:bolder;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .nodeLabel,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edgeLabel{color:#131300;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .label text{fill:#131300;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edgeLabel .label span{background:#ECECFF;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .classTitle{font-weight:bolder;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .node rect,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .node circle,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .node ellipse,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .node polygon,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .divider{stroke:#9370DB;stroke:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 g.clickable{cursor:pointer;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .dashed-line{stroke-dasharray:3;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .dotted-line{stroke-dasharray:1 2;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #compositionStart,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #compositionEnd,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #dependencyStart,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #dependencyStart,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #extensionStart,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #extensionEnd,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #aggregationStart,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #aggregationEnd,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #lollipopStart,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 #lollipopEnd,#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .edgeTerminals{font-size:11px;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-0fb5fa28-8124-411a-8d23-bd76b6169898 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]]UserprototypeUser_prototypeconstructorusername.prototype property
```

### methods

``` js
function User(name){
     this.name = name
}

User.prototype.sayHi = function () {
  return this.name;
};

let user = new User('john');
let user1 = new User('wick');

user.sayHi() 
// 'john'
user1.sayHi();
// 'wick'
```

-   this the main benefit of `prototypes`. you can have inherited
    methods.

``` {style="all:unset;"}
.prototype property#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .error-icon{fill:#552222;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .error-text{fill:#552222;stroke:#552222;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edge-thickness-normal{stroke-width:2px;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edge-thickness-thick{stroke-width:3.5px;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edge-pattern-solid{stroke-dasharray:0;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .marker{fill:#333333;stroke:#333333;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .marker.cross{stroke:#333333;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b g.classGroup text .title{font-weight:bolder;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .nodeLabel,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edgeLabel{color:#131300;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edgeLabel .label rect{fill:#ECECFF;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .label text{fill:#131300;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edgeLabel .label span{background:#ECECFF;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .classTitle{font-weight:bolder;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .node rect,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .node circle,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .node ellipse,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .node polygon,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .divider{stroke:#9370DB;stroke:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b g.clickable{cursor:pointer;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .dashed-line{stroke-dasharray:3;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .dotted-line{stroke-dasharray:1 2;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #compositionStart,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #compositionEnd,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #dependencyStart,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #dependencyStart,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #extensionStart,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #extensionEnd,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #aggregationStart,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #aggregationEnd,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #lollipopStart,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b #lollipopEnd,#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .edgeTerminals{font-size:11px;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-95450bd9-b84d-4d7a-9aa8-744d3767873b :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]]UserprototypeUser_prototypeconstructorsayHiusername.prototype property
```

#### A useful method : reverseString {#a-useful-method--reversestring}

### methods

``` js
function User(name){
     this.name = name
}

User.prototype.reverseName = function () {
  return this.name.split('').reverse().join('');
};

let user = new User('john');
let user1 = new User('wick');

user.reverseName() 
// 'nhoj'
user1.reverseName();
// 'kicw'
```

-   remember *prototype* based *methods* are directly available on their
    created *object instances*.

-   you can also change the *prototype* completely, not recommended
    though

``` js
let animal = {
  eats: true,
  walks: function () {
    return 'walks';
  },
};

function Dog(){
  this.barks = true
}

Dog.prototype = animal;

let dog =  new Dog();

dog.walks() 
// walks

dog.__proto__ === animal;  // true
Dog.prototype === dog.__proto__ // true

```

``` {style="all:unset;"}
.prototype property#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .error-icon{fill:#552222;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .error-text{fill:#552222;stroke:#552222;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edge-thickness-normal{stroke-width:2px;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .marker{fill:#333333;stroke:#333333;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .marker.cross{stroke:#333333;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 g.classGroup text .title{font-weight:bolder;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .nodeLabel,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edgeLabel{color:#131300;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .label text{fill:#131300;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edgeLabel .label span{background:#ECECFF;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .classTitle{font-weight:bolder;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .node rect,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .node circle,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .node ellipse,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .node polygon,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .divider{stroke:#9370DB;stroke:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 g.clickable{cursor:pointer;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .dashed-line{stroke-dasharray:3;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .dotted-line{stroke-dasharray:1 2;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #compositionStart,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #compositionEnd,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #dependencyStart,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #dependencyStart,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #extensionStart,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #extensionEnd,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #aggregationStart,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #aggregationEnd,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #lollipopStart,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 #lollipopEnd,#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .edgeTerminals{font-size:11px;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-f387cf2c-a4aa-4792-ace1-dc3c720508d5 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]]Dogprototypeanimaleatswalks()dogbarks.prototype property
```

## Native Prototypes

-   Object.prototype
-   Array.prototype
-   Function.prototype

### Object.prototype {#objectprototype}

``` js
let obj = {}

let obj1 =  new Object();

Object.prototype === obj1.__proto__ // true
Object.prototype === obj.__proto__ // true
```

-   toString()
-   isPrototypeOf()
-   toLocaleString()

### Array.prototype {#arrayprototype}

``` js
let arr = []

let arr1 =  new Array();

Array.prototype === arr1.__proto__ // true
Array.prototype === arr.__proto__ // true
```

-   push()
-   pop()
-   slice()
-   splice()
-   reverse()
-   \....and many more

### Function.prototype {#functionprototype}

``` js
function Fx(){

}

Function.prototype === Fx.__proto__ // true
```

-   call()
-   apply()
-   bind()
-   arguments
-   caller
-   length

### Date.prototype {#dateprototype}

``` js
let d = new Date();

d.getTime(); // getTime is given by Date.prototype
```

-   getTime()
-   getDay()
-   getDate()
-   \.... more

## Primitives

Primitive types also get wrapped into a Object when used as an Object

### String.prototype {#stringprototype}

``` js
"hello".toString()
```

### Number.prototype {#numberprototype}

``` js
10.1111.toFixed(2)
```

### Boolean.prototype {#booleanprototype}

## Polyfills

-   polyfill is a way of providing futuristic API not available in
    browser.
-   polyfills are made often Native prototype modifications, so that we
    can get a feature/API (which is not available in current browser)
-   This can help us write code / libraries which can run on many
    systems (old or modern)

``` js
if(!Array.prototype.contains){
      Array.prototype.contains = function(searchElement) {
         return this.indexOf(searchElement)>=0 ? true : false          
      }

}
// similar to includes()
```

**NOTE** : `Shims` are piece of code to correct some existing behaviour,
while `Polyfills` are new API/ behaviours.

## Static properties and methods

Some properties and methods are directly created on these Native
constructors.

-   **Object.create()**
-   **Object.keys()**
-   **Object.values()**
-   **Object.hasOwn()**
-   **Array.from()**
-   **Date.now()**

These are not available on instances, and only available on Native
contructors

------------------------------------------------------------------------

# 6. Class {#6-class}

Classes are *easier* way to implement inheritance in JavaScript.

## Syntactic Sugar

It\'s a syntactic sugar to *Protypical Inheritance* BUT more
functionalities than it.

*ProtoType Version*

``` js
function User(name){
     this.name = name
}

User.prototype.sayHi = function () {
  return this.name;
};

let user = new User('john');
user.sayHi() // john
```

*Class Version*

``` js
class User {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    return this.name;
  }
}

let user = new User('john');
user.sayHi() // john
```

### Similarities:

1.  Same kind of *prototype* property with `constructor` method is added
    when called with `new`;
2.  you can use *prototype* also on class based things

``` js
class User {
  constructor(name) {
    this.name = name;
  }

  sayHi() {
    return this.name;
  }
}
User.prototype.sayHello = function(){
    return "hello "+this.name;
}


let user = new User('john');
user.sayHello() // hello john
```

### Differences:

1.  Class methods are *non-enumerable*
2.  Class *toString()* is different
3.  Class can only be called with *new* . Not as a normal function
4.  Class is always is *use strict* mode.

## getter/setters

-   Accessor properties can also be used in class

``` js
class User {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  get fullName(){
      return this.firstName + ' ' + this.lastName;
  }
  set fullName(_fullName){
      this.firstName = _fullName.split(' ')[0];
      this.lastName = _fullName.split(' ')[1];
  } 
}

let user = new User('john', 'wick');
user.fullName // john wick
user.fullName =  "john cena"

user.firstName // john
user.lastName // cena
```

## Computed property names

-   properties which don\'t have a fixed name and assigned by `[ ]`

``` js
let variableName = "hello"
class User {
  constructor(name) {
    this.name = name;
  }

  [variableName]() {
    return this.name;
  }
}



let user = new User('john');
user.hello() // john```
```

## \"this\" binding issue

``` js
class Button {
  constructor(value) {
    this.value = value;
  }

  click() {
    return this.value;
  }
}

let button = new Button("play");

button.click()  // play

setTimeout(button.click, 1000);
// this has issue - this has changed here
```

-   here we lose the context of `this`.

**2 Solution exists :**

1.  Arrow functions : use arrow function wrappers.

``` js
setTimeout(()=>button.click(), 1000);
```

2.  use *.bind()* to `constructor` object.

``` js
setTimeout(button.click.bind(button), 1000);
```

Also you can add this **arrow** style function in class definition -
which will act as class field

``` js
class Button {
  
  constructor(value) {
    this.value = value;
  }

  click = () => { // this is a class field
    return this.value;
  }
}

let button = new Button("play");

button.click()  // play

setTimeout(button.click, 1000);
```

## Inheritance

-   We can inherit Parent Class properties and metods in a Child Class.
    using *extends* keyword

-   Here we have ***Shape*** as *Parent* and ***Rectangle*** as *Child*
    :

``` js
class Shape {
  constructor(name) {
    this.name = name;
  }
  displayShape() {
    return 'Shape ' + this.name;
  }
}

class Rectangle extends Shape {
}

let rect1 = new Rectangle('rect1');

rect1.displayShape(); // Shape rect1

// constructor of Child is implicitly created and it calls constructor of Parent


// constructor(...args){
//     super(..args)
// }
```

``` {style="all:unset;"}
.prototype property#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .error-icon{fill:#552222;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .error-text{fill:#552222;stroke:#552222;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edge-thickness-normal{stroke-width:2px;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .marker{fill:#333333;stroke:#333333;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .marker.cross{stroke:#333333;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 g.classGroup text{fill:#9370DB;fill:#131300;stroke:none;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:10px;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 g.classGroup text .title{font-weight:bolder;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .nodeLabel,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edgeLabel{color:#131300;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edgeLabel .label rect{fill:#ECECFF;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .label text{fill:#131300;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edgeLabel .label span{background:#ECECFF;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .classTitle{font-weight:bolder;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .node rect,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .node circle,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .node ellipse,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .node polygon,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .divider{stroke:#9370DB;stroke:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 g.clickable{cursor:pointer;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 g.classGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 g.classGroup line{stroke:#9370DB;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .classLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .classLabel .label{fill:#9370DB;font-size:10px;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .relation{stroke:#333333;stroke-width:1;fill:none;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .dashed-line{stroke-dasharray:3;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .dotted-line{stroke-dasharray:1 2;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #compositionStart,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #compositionEnd,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .composition{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #dependencyStart,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #dependencyStart,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .dependency{fill:#333333!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #extensionStart,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #extensionEnd,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .extension{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #aggregationStart,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #aggregationEnd,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .aggregation{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #lollipopStart,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 #lollipopEnd,#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .lollipop{fill:#ECECFF!important;stroke:#333333!important;stroke-width:1;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .edgeTerminals{font-size:11px;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 .classTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-4fd0cc83-23da-48bd-96b0-70e7040b6586 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}[[prototype]][[prototype]]ShapeprototypeShape_prototypeconstructornamedisplayNameRectangle_prototypeconstructorrect1Rectangleprototype.prototype property
```

-   Now adding more properties to *constructor* of Rectangle. You have
    to call *super* constructor - which will call *Shape* constructor.

``` js
class Shape {
  constructor(name) {
    this.name = name;
  }
  displayShape() {
    return 'Shape ' + this.name;
  }
}

class Rectangle extends Shape {
  constructor(name, width, height) {
    super(name);
    this.width = width;
    this.height = height;
    this.area = width * height;
  }
}

let rect1 = new Rectangle('rect1', 10, 11);
rect1.displayShape();
rect1.area;
```

## Static Methods

-   We can have *methods* on *constructor* function also.
-   These methods are called *static* methods and they don\'t apply on
    *prototype*. So they are not accessible to created objects also.
-   Use of such methods is limited to Class wide applications
-   *this* remains same as the *class*

``` js
class Shape {
  constructor(name,area) {
    this.name = name;
    this.area = area;
  }
  static areEqual(shape1, shape2){
    return shape1.name === shape2.name && shape1.area === shape2.area
  }

}


let s1 = new Shape('rectangle',100)
let s2 = new Shape('rectangle',100)

Shape.areEqual(s1,s2) // true
```

-   *static* property are also available as a new feature, but rarely
    used.

## Private and Protected properties

-   in Object Oriented Programming there is a concept of *Encapsulation*
    or *Data Hiding* - so that you just interact with object via given
    methods/properties. This avoids changing some internal properties
    which are not meant for public use.

``` js
class User {
  type = "admin" 
  constructor(name) {
    this.name = name;
  }
}

let user = new User('john')
user.type = "normal"
```

-   properties `type` and `name` both are accessible - so they are
    called public

### Protected

-   this is something not provided by javascript but by convention and
    *get/set* method we can create it
-   you have to use convention of *\_* in front of property name -
    making is known to developer that this property is not directly
    accessible and used only via *get/set* accessors.

``` js
class User {
  _type = "admin" 
  constructor(name) {
    this.name = name;
  }
  get type(){
      return this._type
  }
  set type(type){
      this._type = type;
  }
}

let user = new User('john')
user.type = "normal"
```

But what is benefit ?

``` js
class User {
  _type = "admin" 
  constructor(name) {
    this.name = name;
  }
  get type(){
      return this._type
  }
  set type(type){
      if(type==('normal' || 'admin')){
           this._type = type;
      } else {
         throw Error('admin / normal ?')
      }
  }
}

let user = new User('john')
user.type = "normal"
```

### Private

-   this is a new feature and is not very frequently used.
-   you can name any proptery with *\#*

``` js
class User {
  #type = "admin" 
  constructor(name) {
    this.name = name;
  }
  get type(){
      return this.#type
  }
  set type(type){
      if(type==('normal' || 'admin')){
           this.#type = type;
      } else {
         throw Error('admin / normal ?')
      }
  }
}

let user = new User('john')
user.type = "normal"
user.#type // Error
```

## instanceOf

-   to check if object is instance of a Class or inherited from a Class

``` js
class Shape {
  constructor(name) {
    this.name = name;
  }
  displayShape() {
    return 'Shape ' + this.name;
  }
}

class Rectangle extends Shape {
  constructor(name, width, height) {
    super(name);
    this.width = width;
    this.height = height;
    this.area = width * height;
  }
}

let rect1 = new Rectangle('rect1', 10, 11);


rect1 instanceof Rectangle // true
rect1 instanceof Shape // true
```

------------------------------------------------------------------------

# 7. Async JavaScript {#7-async-javascript}

## Asynchronous APIs

-   JavaScript itself is not asynchronous langauge it uses some API from
    browser or enviroment to achieve this behaviour

``` js
console.log(1)
setTimeout(console.log,1000,3); // Timer API
console.log(2)
```

-   Now suppose, we have a function which does something meaningful and
    return a value - but *asynchronously* .

``` js
function sum(a, b) {
    return a + b
}

let asyncFx =(a,b)=>setTimeout(()=>sum(a,b),1000)
```

How to get that value back in program ??

## Callbacks

``` js
function sum(a, b) {
    return a + b
}

let asyncFx = (a,b,cb)=>setTimeout(()=>cb(sum(a,b)),1000)
// callback is passed from outside, and called from inside of async function.

asyncFx(3, 1, function (result) {
    console.log({result}) 
})
```

#### Errors

``` js
function sum(a, b) {
    if(a>0 && b>0){
        return [null,a + b]
    } else{
        return ['input', null]
    }
}

let asyncFx = (a,b,cb)=>setTimeout(()=>cb(...sum(a,b)),1000)

asyncFx(3, 1, function (error,result) {
    if(error){
        console.log({result}) 
    } else{
        console.log({error}) 
    }
})
```

#### Multiple callbacks

``` js
function sum(a, b) {
    if(a>0 && b>0){
        return [null,a + b]
    } else{
        return ['input', null]
    }
}

let asyncFx = (a,b,cb)=>setTimeout(()=>cb(...sum(a,b)),1000)

let x = 4;
let y = 5;

asyncFx(3, 1, function (error, result) {
  console.log({ result });
  asyncFx(x, result, function (error, result) {
    console.log({ result });
    asyncFx(y, result, function (error, result) {
      console.log({ result });          // Callback hell
    });
  });
});
```

## Promise

-   Promise are based on *Publish-Subscribe* pattern.

``` {style="all:unset;"}
Publish Subscriber model#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .error-icon{fill:#552222;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .error-text{fill:#552222;stroke:#552222;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .edge-thickness-normal{stroke-width:2px;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .marker{fill:#333333;stroke:#333333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .marker.cross{stroke:#333333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .cluster-label text{fill:#333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .cluster-label span,#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 p{color:#333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .label text,#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 span,#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 p{fill:#333;color:#333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .node rect,#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .node circle,#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .node ellipse,#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .node polygon,#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .flowchart-label text{text-anchor:middle;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .node .label{text-align:center;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .node.clickable{cursor:pointer;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .arrowheadPath{fill:#333333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .flowchart-link{stroke:#333333;fill:none;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .cluster text{fill:#333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .cluster span,#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 p{color:#333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-0ba263dc-38d1-4f4e-a370-418f496d1246 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}eventeventpublishersubscriber1subscriber2Publish Subscriber model
```

**Example** : Youtube video release

-   *subscribers* are people who are subscribed to channel (with bell
    icon)
-   *publisher* is video uploader channel
-   When the *release event* happens, automatically people are notified
    about the released video.

### Promise constructor

``` js
let promise = new Promise((resolve, reject)=>{
    // async task is inside this
   // if async task is successful
      resolve(data);
   // else task is having error   
      reject(error)
}) 
```

``` {style="all:unset;"}
Promise has many states#mermaid-021919c5-777d-4efb-8ec1-efea07815b24{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .error-icon{fill:#552222;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .error-text{fill:#552222;stroke:#552222;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .edge-thickness-normal{stroke-width:2px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .marker{fill:#333333;stroke:#333333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .marker.cross{stroke:#333333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 defs #statediagram-barbEnd{fill:#333333;stroke:#333333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 g.stateGroup text{fill:#9370DB;stroke:none;font-size:10px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 g.stateGroup text{fill:#333;stroke:none;font-size:10px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 g.stateGroup .state-title{font-weight:bolder;fill:#131300;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 g.stateGroup rect{fill:#ECECFF;stroke:#9370DB;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 g.stateGroup line{stroke:#333333;stroke-width:1;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .transition{stroke:#333333;stroke-width:1;fill:none;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .stateGroup .composit{fill:white;border-bottom:1px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .stateGroup .alt-composit{fill:#e0e0e0;border-bottom:1px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .state-note{stroke:#aaaa33;fill:#fff5ad;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .state-note text{fill:black;stroke:none;font-size:10px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .stateLabel .box{stroke:none;stroke-width:0;fill:#ECECFF;opacity:0.5;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .edgeLabel .label rect{fill:#ECECFF;opacity:0.5;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .edgeLabel .label text{fill:#333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .label div .edgeLabel{color:#333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .stateLabel text{fill:#131300;font-size:10px;font-weight:bold;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .node circle.state-start{fill:#333333;stroke:#333333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .node .fork-join{fill:#333333;stroke:#333333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .node circle.state-end{fill:#9370DB;stroke:white;stroke-width:1.5;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .end-state-inner{fill:white;stroke-width:1.5;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .node rect{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .node polygon{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 #statediagram-barbEnd{fill:#333333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-cluster rect{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .cluster-label,#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .nodeLabel{color:#131300;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-cluster rect.outer{rx:5px;ry:5px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-state .divider{stroke:#9370DB;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-state .title-state{rx:5px;ry:5px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-cluster.statediagram-cluster .inner{fill:white;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-cluster.statediagram-cluster-alt .inner{fill:#f0f0f0;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-cluster .inner{rx:0;ry:0;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-state rect.basic{rx:5px;ry:5px;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-state rect.divider{stroke-dasharray:10,10;fill:#f0f0f0;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .note-edge{stroke-dasharray:5;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-note rect{fill:#fff5ad;stroke:#aaaa33;stroke-width:1px;rx:0;ry:0;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-note rect{fill:#fff5ad;stroke:#aaaa33;stroke-width:1px;rx:0;ry:0;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-note text{fill:black;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram-note .nodeLabel{color:black;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagram .edgeLabel{color:red;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 #dependencyStart,#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 #dependencyEnd{fill:#333333;stroke:#333333;stroke-width:1;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 .statediagramTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-021919c5-777d-4efb-8ec1-efea07815b24 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}resolve(data)reject(error)PendingfullfilledrejectedPromise has many states
```

#### Promise Consumers

``` js
let promise = new Promise((resolve, reject)=>{
    // async task is inside this
   // if async task is successful
      resolve(data);
   // else task is having error   
      reject(error)
}) 


promise.then(successCallback).catch(errorCallback)
```

``` {style="all:unset;"}
then-catch subscribers#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .error-icon{fill:#552222;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .error-text{fill:#552222;stroke:#552222;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .edge-thickness-normal{stroke-width:2px;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .edge-thickness-thick{stroke-width:3.5px;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .edge-pattern-solid{stroke-dasharray:0;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .marker{fill:#333333;stroke:#333333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .marker.cross{stroke:#333333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .cluster-label text{fill:#333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .cluster-label span,#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed p{color:#333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .label text,#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed span,#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed p{fill:#333;color:#333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .node rect,#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .node circle,#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .node ellipse,#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .node polygon,#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .flowchart-label text{text-anchor:middle;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .node .label{text-align:center;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .node.clickable{cursor:pointer;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .arrowheadPath{fill:#333333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .edgePath .path{stroke:#333333;stroke-width:2.0px;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .flowchart-link{stroke:#333333;fill:none;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .cluster text{fill:#333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .cluster span,#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed p{color:#333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(80, 100%, 96.2745098039%);border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-d761b4a1-289d-4ff1-a883-e1ca95e9a2ed :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}resolverejectpromisethencatchthen-catch subscribers
```

#### Callback version

``` js
function sum(a, b) {
    if(a>0 && b>0){
        return [null,a + b]
    } else{
        return ['input', null]
    }
}

let asyncFx = (a,b,cb)=>setTimeout(()=>cb(...sum(a,b)),1000)

asyncFx(3, 1, function (error,result) {
    if(error){
        console.log({result}) 
    } else{
        console.log({error}) 
    }
})
```

#### Promise version

``` js
function sum(a, b) {
  if (a > 0 && b > 0) {
    return [null, a + b];
  } else {
    return ['input not correct', null];
  }
}

let asyncFx = (a, b) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      let output = sum(a, b);
      if (output[0]) {
        reject(output[0]);
      } else {
        resolve(output[1]);
      }
    }, 1000);
  });

asyncFx(-2,4)
.then(data=>console.log(data))  
.catch(err=>console.log(err))
```

## Promise chain

``` js
asyncFx(1, 4)
  .then((data) => {
    console.log(data);
    return asyncFx(1, 4);
  })
  .then((data) => {
    console.log(data);
    return asyncFx(3, 6);
  })
  .then((data) => {
    console.log(data);
  })
  .catch((err) => console.log(err));
```

*Note* : *catch* is only one it catches for all above then. Also note
that `catch` works for `reject` and also any `error` throw by code.

#### finally

``` js
asyncFx(1, 4)
  .then((data) => {
    console.log(data);
    return asyncFx(1, 4);
  })
  .then((data) => {
    console.log(data);
    return asyncFx(3, 6);
  })
  .then((data) => {
    console.log(data);
  })
  .catch((err) => console.log(err));
  finally(()=>{
      doSomething() // after everything is completed
  })
```

## Promise API

### Promise.all {#promiseall}

Parallel execution of async functions - only work when *all promises are
fullfiled*

``` js
Promise.all([
    asyncFx(1,2),
    asyncFx(2,3),
    asyncFx(5,6)
]).then(results=>{
    console.log(results) // array of resolved value, same order
})
```

### Promise.allSettled {#promiseallsettled}

Parallel execution of async functions - only work when *all promises are
fullfiled or rejected*

``` js
Promise.allSettled([
    asyncFx(1,2),
    asyncFx(2,3),
    asyncFx(5,6)
]).then(results=>{
    console.log(results) // array of resolved/reject objects, same order
})
```

### Promise.race {#promiserace}

Parallel execution of async functions - works when *any one of promises
are fullfiled or rejected*

``` js
Promise.race([
    asyncFx(1,2),
    asyncFx(2,3),
    asyncFx(5,6)
]).then(results=>{
    console.log(results) // value of first settled (resolved/rejected) promise
})
```

### Promise.any {#promiseany}

Parallel execution of async functions - works when *any one of promises
are fullfiled*

``` js
Promise.race([
    asyncFx(1,2),
    asyncFx(2,3),
    asyncFx(5,6)
]).then(results=>{
    console.log(results) // value of first fullfilled promise
})
```

### Promise.reject {#promisereject}

created already promise which gets rejected just after creation

``` js
let promise = Promise.reject('error')
```

### Promise.resolve {#promiseresolve}

created already promise which gets resolved just after creation

``` js
let promise = Promise.resolve(123)
```

## Async/Await

-   *async* keywords makes every function to return promise.

``` js
async function sayHi(){
    return "hi"
}

sayHi().then(result=>console.log(result)) // hi
```

-   `"hi"` is wrapped inside using `Promise.resolve`
-   we can use *await* only inside a *async* function
-   *await* is a *syntatic sugar* for Promise *.then()*\*

``` js
function sum(a, b) {
  if (a > 0 && b > 0) {
    return [null, a + b];
  } else {
    return ['input not correct', null];
  }
}

let asyncFx = (a, b) =>
  new Promise((resolve, reject) => {
    setTimeout(() => {
      let output = sum(a, b);
      if (output[0]) {
        reject(output[0]);
      } else {
        resolve(output[1]);
      }
    }, 1000);
  });

async function init() {
  let result = await asyncFx(4, 5);
  console.log({ result });
}

init();
```

### Handling Error in Async/Await function

``` js
async function init() {
  try {
    let result = await asyncFx(4, 5);
    console.log({ result });
  } catch (err) {
    console.log(error);
  }
}

init();
```

-   **async** works for all promise-compatible things

``` js
async function init() {
  let results = await Promise.all([
    asyncFx(1, 2),
    asyncFx(2, 3),
    asyncFx(5, 6),
  ]);
  console.log(results)
}
```

Move to Async Generators ==

------------------------------------------------------------------------

# Property of Object

### 3 criteria to check on every property {#3-criteria-to-check-on-every-property}

1.  `own` or `inherited`
2.  `enumerable` or `non-enumerable`
3.  `String` or `Symbol`

### Property configurations

1.  writeable - `true/false`
2.  configurable - `true/false`
3.  enumberable - `true/false`
4.  value : value of property

``` js
object1 = {property1:42}

Object.defineProperties(object1, {
  property1: {
    value: 42,
    writable: true,
    enumerable: true,
    configurable: true
  },
  property2: {}
});
```

------------------------------------------------------------------------

# Strict Mode

It shows up many *slient* errors in JavaScript.

``` js
'use strict' // file level strict mode


function myStrictFunction() {
  // Function-level strict mode syntax
  "use strict";

}
```

-   *window* global object is not available
-   *assigning* a variable *without declaration* cause issues

``` js
variable = 10
```

-   *duplicate property name* throw error

``` js
let obj = {a:1,a:2}
```

------------------------------------------------------------------------

# Object Constructor API

1.  **Object()** : `new` Object() and Object() are same
2.  **Object.prototype.constructor** : instance of object created will
    have `constructor` set to the reference of creator function. Not
    enumerable

``` js
const o1 = {};
o1.constructor === Object; // true

const o2 = new Object();
o2.constructor === Object; // true

const a1 = [];
a1.constructor === Array; // true

const a2 = new Array();
a2.constructor === Array; // true

const n = 3;
n.constructor === Number; // true
```

3.  **Object.prototype.\_\_proto\_\_** : .

-   it\' simple an accessor property of `Object.prototype`
-   should not be used as `deprecated`
-   use instead `Object.getPrototypeOf` and `Object.setPrototypeOf`
-   It will gave same results are `Array.prototype` if applied on array
    object.

4.  **Object.assign()** : used to copy all the property from source
    object (objects) to a target object.

-   copies `enumerable` and `own` properties ONLY
-   not suitable to copy getter/accessors - as it only copies the value.
-   `String` and `Symbol` both type of properties are copied.
-   Only for `Shallow` Copy

``` js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// Expected output: Object { a: 1, b: 4, c: 5 }

console.log(returnedTarget === target);
// Expected output: true
```

5.  **Object.create()** : creates a new empty object, with an existing
    object as `prototype`

-   should not be used these days, better to use `class` syntax
-   don\'t set contstructor automatically its an issue
-   {} (Object initializer syntax) is syntactic suger to this syntax
    only

``` js
o = {};
// Is equivalent to:
o = Object.create(Object.prototype);

o = Object.create(Object.prototype, {
  // foo is a regular data property
  foo: {
    writable: true,
    configurable: true,
    value: "hello",
    enumerable: true,
  },
  // bar is an accessor property
  bar: {
    configurable: false,
    get() {
      return 10;
    },
    set(value) {
      console.log("Setting `o.bar` to", value);
    },
  },
});
```

``` js
o = Object.create(null);
// Is equivalent to:
o = { __proto__: null };
```

``` js
function Constructor() {}
o = new Constructor();
// Is equivalent to:
o = Object.create(Constructor.prototype);
```

6.  **Object.defineProperties()**: defines new properties or modifies
    old ones,directly on object, return the object

``` js
const object1 = {};

Object.defineProperties(object1, {
  property1: {
    value: 42,
    writable: true,
    enumerable: true,
    configurable: true
  },
  property2: {}
});

console.log(object1.property1);
// Expected output: 42
```

7.  **Object.defineProperty()**: defines a new property or modifies old
    one ,directly on object, return the object

``` js
Object.defineProperty(object1, 'property1', {
  value: 42,
  writable: false
});

object1.property1 = 77;
// Throws an error in strict mode

console.log(object1.property1);
// Expected output: 42
```

8.  **Object.entries()** : array of array of key-value pairs on an
    object proptery (own, enumerable)
9.  **Object.freeze()** : Freezing objects makes properties
    non-writeable and non-configurable.

-   Highest integrity level of JS object. *Object.isFrozen()* checks if
    object is frozen.

10. **Object.fromEntries()** : key-value pairs (inside an iterable,
    array or Map) are converted in object.

-   convert Map to an Object
-   convert Array to an Object
-   tranform object

``` js
// Map to Object
const map = new Map([
  ["foo", "bar"],
  ["baz", 42],
]);
const obj = Object.fromEntries(map);
console.log(obj); // { foo: "bar", baz: 42 }

// Transform object

const object1 = { a: 1, b: 2, c: 3 };

const object2 = Object.fromEntries(
  Object.entries(object1).map(([key, val]) => [key, val * 2]),
);

console.log(object2);
// { a: 2, b: 4, c: 6 
```

11. **Object.getOwnPropertyDescriptor()** : return configuration object
    of a specific property. that object is mutable but won\'t affect the
    original configurations **Object.getOwnPropertyDescriptors()** - is
    similar to this but return configuration of all properties at once.

``` js
const object1 = {
  property1: 42
};

const descriptor1 = Object.getOwnPropertyDescriptor(object1, 'property1');

console.log(descriptor1.configurable);
// Expected output: true

console.log(descriptor1.value);
// Expected output: 42
```

12. **Object.getOwnPropertyNames()** : array of all properties
    *including non-enumberable* but not \"Symbols\" only \"Strings\".
    Similary to this is *Object.getOwnPropertySymbols()* which takes
    only \"Symbols\"

``` js
// Only getting enumerable properties - trick
const target = myObject;
const enumAndNonenum = Object.getOwnPropertyNames(target);
const enumOnly = new Set(Object.keys(target));
const nonenumOnly = enumAndNonenum.filter((key) => !enumOnly.has(key));

console.log(nonenumOnly);
```

13. **Object.getPrototypeOf()** : get the prototype of an Object

``` js
const proto = {};
const obj = Object.create(proto);
Object.getPrototypeOf(obj) === proto; // true
```

14. **Object.hasOwn()** : return true if `own` property.
    *Object.hasOwnProperty()* is older version of same.

``` js
const object1 = {
  prop: 'exists'
};

console.log(Object.hasOwn(object1, 'prop'));
// Expected output: true

console.log(Object.hasOwn(object1, 'toString'));
// Expected output: false

console.log(Object.hasOwn(object1, 'undeclaredPropertyValue'));
// Expected output: false
```

15. **[Object.is](http://object.is/)()** : two values are same or not,
    including primitives

-   Its almost same as `===` but it also differentiate +0 and -0 and NaN

16. **Object.isExtensible()** : true if you can add more properties to
    an object.

17. **Object.prototype.isPrototypeOf()** : check if object exists in
    another object\'s proto chain

``` js
function Foo() {}
function Bar() {}

Bar.prototype = Object.create(Foo.prototype);

const bar = new Bar();

console.log(Foo.prototype.isPrototypeOf(bar));
// Expected output: true
console.log(Bar.prototype.isPrototypeOf(bar));
// Expected output: true
```

18. **Object.keys**() : array of keys (own, enumberable, string type)

19. **Object.preventExtensions()** : prevents adding of new properties,
    also prevents re-assignment of prototype value.

20. **Object.prototype.propertyIsEnumerable()** : check if `enumerable`
    own property.

21. **Object.seal()** : seals objects for further addition of new
    properties, and also make `configurable: false` for all properties.
    but allow old property value modifications.

22. **Object.setPrototypeOf()** :

``` js
const obj = {};
const parent = { foo: 'bar' };

console.log(obj.foo);
// Expected output: undefined

Object.setPrototypeOf(obj, parent);

console.log(obj.foo);
// Expected output: "bar"
```

23. \*\*Object.prototype.LocaleString() :

``` js
const date1 = new Date(Date.UTC(2012, 11, 20, 3, 0, 0));

console.log(date1.toLocaleString('ar-EG'));
// Expected output: "٢٠‏/١٢‏/٢٠١٢ ٤:٠٠:٠٠ ص"

const number1 = 123456.789;

console.log(number1.toLocaleString('de-DE'));
// Expected output: "123.456,789"
```

24. **Object.prototype.toString()** : for converting object in String
    format
25. **Object.prototype.valueOf()** : for converting Object in primitive
    values by when primitive value is expected.
26. **Object.values**() : array of vaules (own, enumberable,string
    keyed)

::: {.mermaidTooltip style="opacity: 0;"}
:::
