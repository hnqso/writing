# React Components

*Content of my light talk at [Moo Tech Tuesday](https://www.eventbrite.co.uk/e/the-new-shiny-javascript-development-in-2016-tickets-25196915653) on Tue, 31 Feb 2016. It contains some extra bits I left out because of timing. You can find the slides on [Speaker Deck](https://speakerdeck.com/henriquea/react-components-playing-simple-and-easy)*

I've been working on a range of React products from FX/trading tools to CRM and online booking. Here are just a few of the good patterns I found so far while building small, medium and large apps with React.

## Playing easy and simple

I like football, a play twice a week. One the phrases I hear most is *"Hey man! Play simple"*. One thing I can tell you: play simple football is hard.

The same for components, keep them simple and easy it's hard work.

## Hello React

One thing I love about is React **it enables and embraces modularity** making things easier for us. We can use the pillars of functional programming to build powerful components: pure functions, immutability, high order functions and composition.

## Low level components

We shouldn't create a new component every time we want to build a new UI.

The idea around low level components isn't new. Take the `View` in React Native. It maps directly to the native view equivalent `UIView`, `<div>`, etc.

In this example the `<Image>` maps to the `<img>` HTML element.

```js
// layout/image.js
// e.g. <Image src="cover.png"/>
const Image = ({...props }) => (
  <img {...props} />
);
```

In the example bellow the `CoverImage` component becomes bloated when adding more props.

```js
const CoverImage = ({title, src}) => (
  <img src={src} alt=`${title}` />
);
```

Rather drop a `img` tag everywhere we create a low level component `<Image>`. Now we can pass all the element default attributes and any other props.

```js
// layout/image.js
const Image = ({...props }) => (
  <img {...props} />
);

// components/cover-image.js
const CoverImage = ({title, src}) => (
  <Image
    src={src}
    alt=`${title}`
  />
);
```

Now we have a composable component which is easy to maintain. We can place it anywhere in our application.

Low level components don't hold any business logic or styling unless you need normalise the element cross browsers.

```js
// image.js
const Image = ({...props }) => {
  const style = {
    borderStyle: 'none'
  };
  const styles = Object.assign({},
    style,
    props.style
  );
  return <img {...props} style={styles} />
};
```

## Component healthy with propTypes

You know what the component does by looking at its `propTypes`.

```js
import React, { PropTypes } from 'react';

BookItem.propTypes = {
  coverImage: PropTypes.element.isRequired,
  title: PropTypes.string.isRequired,
  author: PropTypes.string.isRequired,
  description: PropTypes.string,
  price: PropTypes.number.isRequired
};
```

The only catch here is: `propTypes` are not statically analyzable. You will only find a problem when the component has rendered.  Likely to happen when it hit the production in a sunny Friday afternoon while people are heading to the pub.

Thankfully we can use [Flow](http://flowtype.org/) for type checking:

```js
type Props = {
  coverImage: CoverImage,
  title: string,
  author: string,
  description?: string,
  price: number
};

const BookItem = ({
  coverImage,
  title,
  author,
  description,
  price,
  ...props
}: Props) => (
  // Magic here!
);
```

Flow helps catch errors early and improves the code readability.

## A flat component structure

A simple structure make things easy to remember and brings consistency. When possible I like to have a flat structure for my components.

Having the `index.js` as entry point is standard in the node ecosystem but also makes the import path shorter `./components/book-cover`.

```
book-cover/
  index.js
  book-cover.js
  book-cover.css
  book-cover-tests.js
  book-cover-fixtures.js
```

However I understand this might turn into a [tabs versus space](https://www.youtube.com/watch?v=SsoOG6ZeyUI) drama and possible fight.

## Styling

For consistency all root elements have the same selector name `.root`. The same happens to modifiers.

```css
/* button.css */
.root {}
.selected {}

/* dropdown.css */
.root {}
.selected {}
```

This is one of the greatest things about modular CSS. It doesn't enforce you a naming convention. I don't have to think about it.

When possible, I make a choice to go back to the origins where CSS were for styling a document only. What this means is:

> Any styling logic lives in the component not in the CSS.

I use either [CSS Modules](http://glenmaddern.com/articles/css-modules) or Inline Styles with [JSS](https://github.com/jsstyles/jss) or [Aphrodite](https://github.com/Khan/aphrodite). Let's say I want the button text to be bolder. I can use `composes` right?

```css
/* button.css */
.root {
  composes: bolder from 'typography';
}
```

Well, not really.

> I avoid composition in CSS when possible.

This becomes redundant with React. We can easily compose the button using the `<Text>` component.

```js
const Button = () => (
  <div className={styles.root}>
    <Text weight="bold">Button</Text>
  </div>
);
```

Michele Bertoli suggested an interesting approach [Atomic CSS Modules](https://medium.com/yplan-eng/atomic-css-modules-cb44d5993b27)
combining both Atomic CSS and CSS Modules. I can see myself using `compose` in this case.

## Helpers for inline styles

Helpers are pretty awesome. They're like mixin in Sass but way more powerful because it's JavaScript. Also they work well with Aphrodite or JSS.

```js
// gradient.js
export const linearGradient = (a, b) => ({
  background: `linear-gradient(
    to bottom,
    ${a},
    ${b}
  )`
});

// button.js
const styles = {
  ...linearGradient('#eee','#ddd'),
  padding: 8
};
```

[Kristjian Ristovski](https://twitter.com/kitze) made some useful [helpers](https://github.com/kitze/stylz/tree/master/test/helpers). He's also exploring some ideas around advanced animation.

## Final thoughts

We have a bunch of clever people trying to solve the same problems using different approaches. So:

- Don’t be religious
- Don’t knock it without try
- Pick the one that works better for your team

At the end of the day we are all together trying to delivery the best product for our users.

{% assign url = page.url | prepend: site.url %}
<a href="https://twitter.com/intent/tweet?text={{page.title}}&url={{url}}&via=healves82" class="share">
  <i class="icon"><svg data-icon="twitter" viewBox="0 0 32 32" style="fill:currentcolor">
    <path d="M2 4 C6 8 10 12 15 11 A6 6 0 0 1 22 4 A6 6 0 0 1 26 6 A8 8 0 0 0 31 4 A8 8 0 0 1 28 8 A8 8 0 0 0 32 7 A8 8 0 0 1 28 11 A18 18 0 0 1 10 30 A18 18 0 0 1 0 27 A12 12 0 0 0 8 24 A8 8 0 0 1 3 20 A8 8 0 0 0 6 19.5 A8 8 0 0 1 0 12 A8 8 0 0 0 3 13 A8 8 0 0 1 2 4"></path>
  </svg></i> <span>Share this on Twitter</span>
</a>
