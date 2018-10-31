# [DEMO](typetura-js.netlify.com)

This is a tool to make fluidly responsive typography easy.

# How to use:

* Link letterset.js in your `<head>`.
* Start styling with CSS.

### Starting with the basics

At its core, Typetura works with [CSS keyframe animations](https://developer.mozilla.org/en-US/docs/Web/CSS/@keyframes) and ties those animations to the width of the page or [an element](#Work-off-the-width-of-an-element-and-more) instead of a timeline. Let’s create keyframes for our `<h1>`.

```css
@keyframes h1 {
  0%,20% {
    font-size: 1.2em;
  }
  100% {
    font-size: 4em;
  }
}
```

Now that you have your keyframes set up, let’s tell typetura to use those keyframes to scale the text.

```css
h1 {
  --tt-key: h1;
}
```

Awesome! You should be seeing typetura working. But you might be thinking the effect is happening over too wide a range. By default, the keyframes map to a viewport range of `0px` to `1600px` wide. Change the max to `960px` adding `--tt-max:960;` either locally on the `h1` or globally on the `body`.

So far, your CSS should look somthing like this:

```css
h1 {
  --tt-key: h1;
  --tt-max:960;
}

@keyframes h1 {
  0% {
    font-size: 1.2em;
  }
  100% {
    font-size: 4em;
  }
}
```

At this point you may be noticing the fluid transition cuts off at that `960px` width we set earlier. This is because the animation has stopped and the normal `h1` value is currently being used. Move the value(s) from the `100%` keyframe to your `h1`. Just like with regular CSS animations, the animation transitions into the values defined on the element so we can safely delete that keyframe and below is our final CSS for our `h1`.

```css
h1 {
  font-size: 4em;
  --tt-key: h1;
  --tt-max:960;
}

@keyframes h1 {
  0% {
    font-size: 1.2em;
  }
}
```

Anything that can be animated can be used in these keyframes like color, transforms, size, margins, padding, variable font properties, etc. The sky is the limit.

### Work off the width of an element and more

By default typetura queries the width of the `body` element but you can select any other element, like an `article` element. To do this, add `id="typetura"` to the element you wish to use as the width reference.

Typetura can also work with any unit-less number you feed it. You can bind it to scroll depth, cursor position, device orientation, or ambient light. To do this, pass the values through the CSS property `--tt-bind`. This value inherits so you can set it on the `body` if you want it to be applied everywhere or on a specific element. [Momentum](https://github.com/scottkellum/momentum) is a library that exposes a number of these events for you to use. If you were using [Momentum](https://github.com/scottkellum/momentum) with typetura you could write `body {--tt-bind:--scrolly}` to bind typetura to scroll instead of viewport width.

### Custom easing

Easing works in typetura just like it does with any other animations. However you may want the easing functions you set to inherit and the default timing functions don’t. You can set your timing functions in typetura with `--tt-ease` and that timing function will be inherited by any element underneath it.

### Index

<table>
  <tr>
    <th>Property
    <th>Accepted values
    <th>Inherits
    <th>Default value
<tr>
  <td><code>--tt-key</code>
  <td><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/animation-name">The keyframes name (string)</a>
  <td>no
  <td><code>''</code>
<tr>
  <td><code>--tt-max</code>
  <td>Value at witch the animation ends (number)
  <td>yes
  <td><code>1600</code>
<tr>
  <td><code>--tt-ease</code>
  <td><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function">Animation easing function</a>
  <td>yes
  <td><code>linear</code>
<tr>
  <td><code>--tt-bind</code>
  <td>Position of the animation between <code>0</code> and <code>--tt-max</code> (number)
  <td>yes
  <td><code>--tt-width</code>