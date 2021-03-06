# Potions

<img align="right" width="500" src="./src/potions-light.svg?sanitize=true#gh-light-mode-only">
<img align="right" width="500" src="./src/potions-dark.svg?sanitize=true#gh-dark-mode-only">

## Design

The first mock-up was a very rough sketch on a post-it note. I'm no artist, but I liked it enough to keep going. So I patched together a mood board of various designs, in a folder on my desktop, booted-up some illustration software and got started...

Additionally, there's some amazing artists out there. If you know where to look, there's influential creativity everywhere. (E.g. [Dribbble](https://dribbble.com/shots/5781741-Potion-of-Wisdom-Speedpaint), [Reddit](https://www.reddit.com/r/Design/comments/b68bvu/heres_a_quick_breakdowntutorial_on_how_i_animate/), [Artstation](https://www.artstation.com/artwork/9m18kN), ...)

## Inkscape

On the topic of illustration software, there are a few options to choose from. I've used a trial of Adobe Illustrator before, which was excellent, but not remotely worth it's cost or contract lock-in. So I gave [Inkscape](https://inkscape.org/) a try. It turned out to be a great piece of software, and open-source which is always amazing. Albeit, it could use a bit more documentation and a few official tutorials. But, that only meant it needed some exploring...

One excellent feature of Vector Graphic tools is the clipping mask. It unlocks a huge number of possibilities for animations, as you can create a complex shapes in a background layer and send objects across the gap. This allows certain objects to leave the apparent field of view; by matching the colour of the mask to the webpage background. (E.g. The blue multi-hexagon shape of `potions.svg` was cut-out, and has a periodic, sweeping line rotating across the gap). To create a clipping mask:

- Draw your background layer
- Draw your cut-out shape
- Set the colour of your cut out shape to Black (#000000). Or lighten the colour if you wish your cut-out to be partially faded.
- Select both
- Navigate to `Object` --> `Mask` --> `Set Inverse (LPE)`

Also, since Inkscape saves vector graphics in their own personalised format, here are a few steps I created to convert it for code use:

- Using Inkscape, add labels to all the relevant shapes/groups in the `Objects Pane` (only required once)
- Using a text editor, replace all: `inkscape:label=` with `class=`
- Upload it to [SVGOMG](https://jakearchibald.github.io/svgomg/). An excellent tool, utilizing [SVGO](https://github.com/svg/svgo) to optimise and prettify SVGs.
- Add the CSS (detailed below)

## Animation

CSS can be easily included in SVGs using the `<foreignObject>` tag. Simply insert this block of code under the initial `<svg>` line and you're set.

```html
<foreignObject>
  <div xmlns="http://www.w3.org/1999/xhtml">
    <style>
      /// CSS HERE
    </style>
  </div>
</foreignObject>
```

## Dark Mode Detection

Since GitHub has a dark mode, we need to account for that in the design. The obvious solution is the CSS property `prefers-color-scheme`, launched in 2019. Luckily, it can be handled using some fairly simple media queries in our CSS. For instance:

<!-- prettier-ignore -->
```css
@media (prefers-color-scheme: light) {
  .Background  { fill: #fff }
}
@media (prefers-color-scheme: dark) {
  .Background  { fill: #0d1117 } 
}
```

However, it no longer works on GitHub, and is most likely deliberately not supported. Fortunately, an alternative method of dark-mode detection does exist; specific to [GitHub flavoured markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#specifying-the-theme-an-image-is-shown-to). Still, it does come with some caveats. It requires two files, and may not always work when the readme is viewed from an external source. (E.g. [NPM](https://www.npmjs.com/), [crates.io](https://crates.io/), ...). But neither is a significant problem in this instance.

```
![Potions](./potions-light.svg#gh-light-mode-only)
![Potions](./potions-dark.svg#gh-dark-mode-only)
```

## Acknowledgements

- [illlustrations.co](https://illlustrations.co/)
- [Inkscape](https://inkscape.org/)
- [SVGO](https://github.com/svg/svgo)
- [CSS in README](https://github.com/sindresorhus/css-in-readme-like-wat)
