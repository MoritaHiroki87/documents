# CSSの書き方

```css
@charset "UTF-8";

/* ---------------------------------
全体適用CSS
 --------------------------------- */
html{
  font-size: 62.5%;
}
body{
  color:#333;
  font-size:1.2rem;
  font-family:"Hiragino Kaku Gothic ProN", Meiryo, sans-serif;
  margin: 0;
}
*, *::before, *::after{
  box-sizing:border-box;
}
a:link, a:visited, a:hover, a:active{
  columns: #d03c56;
  text-decoration:none;
}
.clearfix::after{
  content: "";
  display: block;
  clear: both;
}


```
