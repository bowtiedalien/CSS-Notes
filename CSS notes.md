<header> 

<link href="https://fonts.googleapis.com/css?family=Rakkas" rel="stylesheet">

<link href="CSS-notes.css" rel="stylesheet" type="text/css">

<link href="https://afeld.github.io/emoji-css/emoji.css" rel="stylesheet">

</header>

# CSS notes

<h2 id="index-heading">Index</h2>
<div id="index">

- [Colours](#identifiable-color-names)

- [WebFonts](#where-to-find-web-fonts)

- [Clockwise Notation for Padding/Margin](#padding/margin-clockwise-notation)

- [Inheritance in CSS](#inheritance-and-overriding-styles)

- [Variables](#variables)

- [CSS Grids](#css-grids)

  - [Media Queries](#media-queries)
  - [Aligning items in a Grid cell](#aligning-an-item-inside-its-cell)
  - [Justification and Alignment in CSS](https://alligator.io/css/align-justify/)
  - [Changing grid column width responsively](#responsive-grid-columns)
    

</div>

<br/>

### What does CSS allow you to do? 
- allows you to control
  - color 🎨
  - fonts 🖌
  - positioning 📍
  - spacing 📐 
  - sizing 🔎
  - decorations 🎊
  - transitions 🙈 🙉 🙊

## identifiable colour names:
- <span style="color:red">red</span>
- <span style="color:yellow">yellow</span>
- <span style="color:blue">blue</span>
- <span style="color:green">green</span>
- <span style="color:salmon">salmon</span>
- <span style="color:pink">pink</span> 
- <span style="color:orange">orange</span>
- <span style="color:gold">gold</span>

lots more <a href="https://www.w3schools.com/cssref/css_colors.asp">here</a> !

**Note:** more specific colour tones can be added using *hex color codes* and *RGB colour codes*.

to add a hex colour:
```css
{
color: #FF00FF
}
```
to add an RGB colour:
```css
{
color: rgb(255,0,255);
}
```

## How to link to a stylesheet:

```html
    <link rel="stylesheet" type="txt/css" href=" ">
```

## Where to find Web Fonts 

https://fonts.google.com/

decide what web fonts to pair together:

https://fontpair.co/

how to use fonts in your stylesheet:

1. import the font like this:
```css
<link href="https://fonts.googleapis.com/css?family=Cairo" rel="stylesheet">
```
2. start using it in any style like this:
```css
font-family: 'Cairo'
```

also check this:

[helpful link on khanacademy about styling using web fonts](https://www.khanacademy.org/computer-programming/google-web-fonts-example/6665372888072192)

## Padding/Margin Clockwise Notation

instead of doing this:
```css    
p{
    padding-right: 10px;
    padding-left: 5px;
    padding-top: 5px;
    padding-bottom:10px;
}
```
we can immediately do this:
```css
    p{
        padding: 5px 10px 10px 5px;
    }
```
where the order is: top, right, bottom, left. Clockwise!

## Inheritance and overriding styles

Rules:
- classes override inherited styling from the `<body>` tag
- IDs override classes. 
- lower classes in the `<style>` tag override higher classes
- inline styles override anything in the `<style>` tag
- keyword `!important` overrides everything. Place it next to a style
    ```css
    .pink-text{
    color: pink !important
    }
    ```
 and it will always be executed no matter how many times it is overriden later in the code

## Variables 

 you can use variables to apply the same style to multiple attributes at once, like so:
 ```css
 .penguin{
     --penguin-skin: grey; /*declaration*/
 }
 .penguin-top{
     background: var(--penguin-skin, grey); /*usage*/
 }
 ```
 the second argument inside the `var()` brackets is the _fallback value_. If we can not use the variable for whatever reason (be it the variable name is spelled wrong or someone is using an old browser that does not use CSS variables), the browser will execute this value.

 **Note:** variables are available inside the element in which you declare them. In order to make variables available throughout the stylesheet, define them in the `root` element.
```css
:root{
    --penguin-skin:black;
}
```
**Note2:** variables can be overriden in specific elements individually. For example, if `--penguin-skin` is used in `.penguin-top`, we can override it inside `.penguin-top` individually and make the colour grey instead.

```css
.penguin-top{
    --penguin-skin:grey; /*overriding*/

    color: var(--penguin-skin,grey);
}
```
### Media Queries ### 
definition: media queries can be used to change variables depending on the size of the screen. 
```css
@media(max-width:350px)
{
    :root{
        --penguin-size:200px;
        --penguin-skin:black;
    }
}
```
so now when you change the size of the browser window and make it small enough to be 350px, the penguin will be smaller and its skin will be black. As long as its bigger than 350px, this media query will not apply.

*Remark*: Usually, we care about adjusting the layout for two screen width:
1. smartphone layout: min-width(480)
2. desktop layout: min-width(1024)

## CSS Grids

definition: Grids make it really easy to 
1. place elements wherever you want them on a webpage
2. rearrange elements (for Responsive Web Design) in different sized screens
3.maintain and easily reach any of those elements in the code (leads to a clean code!) 

how to define a certain `div` as a grid + all the related properties:
```css
.container{
    display:grid; /*declares the grid*/

    grid-template-columns: auto 1fr 2em; /*grid contains 3 columns*/

    grid-template-rows:auto 30% 10px; /*grid contains three rows*/

    grid-template-areas:
    "[enter names of areas inside the grid here]";

    grid-column-gap: 20px; /*if you would like some space between your grid elements instead of being laz2een f ba3d*/

    grid-row-gap: 10px; /*gaps between columns*/
}
```

**Note:**
1) setting a column as `auto` means that it will be as wide as it needs to be for elements to fit in exactly
2) a shorthand property for `grid-column-gap` and `grid-row-gap` is `grid-gap`:
```css
{
    grid-gap: 10px 20px; /*rows columns*/
}
```
3) you can use a period in `grid-template-areas` to represent an empty cell
```css
{
    grid-template-areas: 
    "header header header"
    ". content content"
    "footer footer footer"
}
```
4) to let elements span areas without defining `grid-template-areas`, you can use column and row spanning:
```css
.item1{
    grid-column:1/3;
    grid-row:1/3;
}
```
Now this element will take the first two columns and the first two rows. 

*tip*: refer to this picture when you're doing col/row spanning 👇 (remember: the numbers are for the hypothetical lines between the areas NOT for the areas themselves)

<img src="grid-placement.png" alt="grid placement.png">

**Note:** you can also still define areas for the elments without setting up area names (i.e. `grid-template-areas`): 

```css
.item1{
    grid-area:1/1/1/5; 

    /*refer to the attached image and notice this will actually make the element take up the header of the grid.*/
}
```

### aligning an item inside its cell

a cell is the place an element or an item is set to reside in inside a grip. Or in other words, it is the *area in a grid* where an element is present.
By default, the align property has a value of stretch, which will make the content fill the whole width of the cell. However, we can align the content either `start`, `end` or `center`.

```css
item1{
    justify-self:left; /*align horizontally*/
    align-self:start; /*align vertically*/
}
```
*Remark:* if you want all the items in a grid to share the same alignment, use `justify-items` and `align-items` in the parent container.

```css 
.container{
    justify-items:center;
    align-items:end;
}
```
### responsive grid columns [^summarised]

instead of defining a fixed number of columns for a grid, we can let the browser decide how many columns with a fixed width can fit within the current display width. This is super cool for RWD (responsive web design) purposes!
```css
.container{
    grid-template-columns: repeat(auto-fill, minmax(90px,1fr));

}
```
what this is saying:
create as many columns as you can in a given display with the width of the columns always being 90px as a minimum value or 1fr of the display as a maximum value.

**Note:** you can also use `auto-fit` instead of `auto-fill` and they will do the same thing except for the fact that `auto-fit` will make sure your columns always stretch up to take the whole width of the display, while `auto-fill` does not necessarily ensure that.

*Observation:* Rand Morten adviced: "first build the whole website for mobile display, and use that as a fallback if the browser does not support grids." In addition to that, building the website first as mobile version, we can later test for `min-width` using media queries and responsively change the layout. Bottomline, do start with the mobile version because this is the worst case scenario where all your bigger layouts might fail, then use queries and start expanding from there.


[^summarised]: this section is a compression of multiple sections from the ref video. 

    Section Index (click to jump to topic):
    
    1. <span class="small-links">[Using the Repeat Function](https://youtu.be/ieTHC78giGQ?t=3763)</span>
    2. <span class="small-links">[Using the minmax function](https://youtu.be/ieTHC78giGQ?t=3894)</span>
    3. <span class="small-links">[Using auto-fill](https://youtu.be/ieTHC78giGQ?t=3948)</span>
    4. <span class="small-links">[Using auto-fit](https://youtu.be/ieTHC78giGQ?t=3999)</span>

References:
1. [CSS Grid Changes Everything by Morten Rand Hendriksen](https://www.youtube.com/watch?v=7kVeCqQCxlk)