### 快速上手
- 在vue中使用
```
1.安装
npm install less less-loader -S
2.配置webpack
webpack.base.conf.js中的
module:{
    rules:[
        {
            test:/\.less$/, //匹配后缀名
            loaders:"style-loader!css-loader!less-loader" //指定loader
        }
    ]
}
3.npm run dev
4.<style scoped lang="less">
5.常用语法
@btn-bgColor:blue; //定义变量，后面要加分号（暂时不知如何支持默认值）
.page01{ //嵌套语法
    .nav{
        a{
            color:@btn-bgColor;
            &:hover{color:#fff;} //&代表父标签，定义hover时
        }        
    }
    .container{
        .blueBtn,.redBtn{font-size:16px;} //群组选择器
    }
    .footer{
        // background{    //暂时不知如何支持属性嵌套            
        //     color:#fff;
        //     repeat:no-repeat
        // }
        background-color: #fff;
        background-repeat: no-repeat;    
    }
}
```
- 单独使用
```
npm i -g less
$ lessc styles.less styles.css
压缩编译
npm install -g less-plugin-clean-css
lessc --clean-css styles.less styles.min.css
单独使用无法批量编译
无法实时编译
```
---
### 语法
```
感觉和sass相比，less多了一些函数方法，和属性计算。
```
- 变量（variables） @
```
@width: 10px;
@height: @width + 10px;
#header {
  width: @width;
  height: @height;
}
为
#header {
  width: 10px;
  height: 20px;
}
```
- 混合（mixins）
```
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
#menu a {
  color: #111;
  .bordered();
}
.post a {
  color: red;
  .bordered();
}
```
- 嵌套（Nesting）
```
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
    a{
        color:#fff;
        &:hover{color:#000;}
    }
  }
}
在@media or @supports中的使用
.component {
  width: 300px;
  @media (min-width: 768px) {
    width: 600px;
    @media  (min-resolution: 192dpi) {
      background-image: url(/img/retina2x.png);
    }
  }
  @media (min-width: 1280px) {
    width: 800px;
  }
}
为
.component {
  width: 300px;
}
@media (min-width: 768px) {
  .component {
    width: 600px;
  }
}
@media (min-width: 768px) and (min-resolution: 192dpi) {
  .component {
    background-image: url(/img/retina2x.png);
  }
}
@media (min-width: 1280px) {
  .component {
    width: 800px;
  }
}
```
- 运算（Operations）
```
单位能用+, -, *, / 符号
如：
// numbers are converted into the same units
@conversion-1: 5cm + 10mm; // result is 6cm
@conversion-2: 2 - 3cm - 5mm; // result is -1.5cm

// conversion is impossible
@incompatible-units: 2 + 5px - 3cm; // result is 4px

// example with variables
@base: 5%;
@filler: @base * 2; // result is 10%
@other: @base + @filler; // result is 15%
```
- Escaping
```
@media (min-width: 768px) {
  .element {
    font-size: 1.2rem;
  }
}
为
@min768: (min-width: 768px);
.element {
  @media @min768 {
    font-size: 1.2rem;
  }
}
```
- 函数（Functions）
```
如percentage  saturate
@base: #f04615;
@width: 0.5;

.class {
  width: percentage(@width); // returns `50%`
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
```
- Namespaces and Accessors
```
#bundle() {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white;
    }
  }
  .tab { ... }
  .citation { ... }
}
取部分
如：
#header a {
  color: orange;
  #bundle.button();  // can also be written as #bundle > .button
}
```
- 作用域（Scope）
```
@var: red;
#page {
  @var: white;
  #header {
    color: @var; // white
  }
}
```
- 注释（Comments）
```
/* 一个块注释
 * style comment! */
@var: red;

// 这一行被注释掉了！
@var: white;
```
- 导入（Importing）
```
@import "library"; // library.less
@import "typo.css";
```
- 安装
```
npm i less -D
```
```
~""//避免编译
```