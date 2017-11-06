# Workflows with Icons

--

## Sitemap

1. Brief Overview 
  - SVG Sprites as background image
  - Embed Data-URI in CSS
  - Icon fonts
2. Missing pieces
  - Inline svg sprites
3. Discussion

---

## SVG Sprites as background image

--

### Tasks

Just save every SVG file into the folder `resources/assets/img/svg/icons`. 

Then execute `grunt sprites`.

--

### Output

You will get a scss file with mixins in there: 

```scss
@mixin sprites-arrow_double() {
	@include sprites-bg-size;
	@include sprites-bg-svg;
	width: 15px;
	height: 12px;
	background-position: -485px 0;
	@at-root .no-svg & {
		@include sprites-bg-png;
	}
}
```
--

### Pro
- Easy to use
- pure CSS
- easy to cache
- multiple colors per icon
- PNG fallback

--

### Contra 
- no color transition
- multiple same items

---

## Embed Data-URI in CSS

--

### Tasks

Just save every SVG file into the folder `resources/assets/img/svg/icons`. 

Then execute `grunt icons`.

--

### Output

You will get multiple scss file with mixins and extends in there: 

```scss

@mixin icon-agency-contact_address {
	background-image: url('data:image/svg+xml...');
	background-repeat: no-repeat;
}

```
--

### Pro
- Easy to use
- pure CSS
- easy to cache
- multiple colors per icon
- PNG fallback

--

### Contra 
- larger file size
- no color transition
- multiple same items

---

## Icon Fonts

--

### Tasks

Just save every SVG file into the folder `resources/assets/img/svg/icons`. 

Then execute `grunt webfont-icons`.

--

### Output

You will get a scss file and font files. the scss contains classes:  

```scss
@font-face {
	font-family:"vw-icons";
	src:url("../fonts/vw-icons.eot?7931d8204e18ae44bd174526daf5527b");
	src:url("../fonts/vw-icons.eot?#iefix") format("embedded-opentype"),
		url("../fonts/vw-icons.woff?7931d8204e18ae44bd174526daf5527b") format("woff"),
		url("../fonts/vw-icons.ttf?7931d8204e18ae44bd174526daf5527b") format("truetype");
	font-weight:normal;
	font-style:normal;
}

.icon {
	font-family:"vw-icons";
	display:inline-block;
	vertical-align:middle;
	line-height:1;
	font-weight:normal;
	font-style:normal;
	speak:none;
	text-decoration:inherit;
	text-transform:none;
	text-rendering:auto;
	-webkit-font-smoothing:antialiased;
	-moz-osx-font-smoothing:grayscale;
}

.is-icon-close:before {
	content:"\f105";
}
```
--

### Pro
- Easy to use
- scalable with font size
- color transitions

--

### Contra 
- extra font files
- only one color possible
- usage of width and height is not possible
- Accessibility
- loading time can lead to a display of unexpected characters

---

## Inline SVG Sprites :: Grunticon

--

### Grunticon

You can use the option `enhanceSVG` to create the following demo output: 

```html
<div class="icon-burger alt" data-grunticon-embed></div>
```

After integrating the script of the Filament Group you get the following HTML: 

```html
<div style="background-image: none;" class="icon-burger alt">
  <svg class="svg-source" xmlns="http://www.w3.org/2000/svg" width="32" height="30" viewBox="170.6 12.6 32 30" enable-background="new 170.6 12.6 32 30">
    <g class="hamburger">
      <path class="buns" fill="#DDAF6D" d="M188.6 12.6h-4c-5.5 0-13 4.5-13 10v1c0 .6.4 1 1 1h28c.6 0 1-.4 1-1v-1c0-5.5-7.5-10-13-10zm-17 28c0 1.1.9 2 2 2h26c1.1 0 2-.9 2-2v-2h-30v2z">
      </path>
      ...
    </g>
  </svg>
</div>
```

--

### Pro
- CSS with enhancement
- inline svg
- multiple colors per icon
- color transitions

--

### Contra 
- larger file size
- it is not so easy to use

---

## Inline SVG Sprites :: SVG Store

--

### SVG Store

You can use another plugin which is just creating a svg file with proper attributes. 

```hbs
{{{svg}}}

{{#each icons}}
    <svg>
      <use xlink:href="#{{name}}" />
    </svg>
{{/each}}
```

--

### Pro
- Real inline svgs
- multiple colors per icon
- color transitions

--

### Contra 
- no fallback
- deprecated

---

## Discussion

![alt Questions](assets/img/questions-bale.gif "Questions")