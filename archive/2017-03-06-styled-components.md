# Styled components

## The first time

Part of this post is from a GitHub issue I created to discuss component styling with the team at [Moteefe](https://www.moteefe.com/).

The first time I heard about [styled-components](https://styled-components.com/) my reaction was:

> 🤔 ... 💩

At the same time I wanted to give it a fair shot before dismissing it. The best way to measure any tool is by using it.

I'm currently building a ticket sales system and decided to use styled-components. I must admit: I was wrong. The developer experience is great.

The first reason why I decided to use it in this project was because I didn't want to eject `create-react-app` or to use a custom react-scripts fork just to enable CSS modules.

It's early day for me but the benefits I had straight-away by using them are:

## No learning curve, you are writing CSS

At first styled-component may feel over-engineered but how this is different from CSS?

```js
const ErrorMessage = styled.ul`
  padding: 10px 16px;
  color: #f18d8d;
  background-color: #fff2f2;
  border-radius: 3px;
`
```

It isn't. It's just CSS string inside a [template literal](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Template_literals).

## It enforces composition

When you need to apply style to a HTML element you have to break it down into small components.

```js
const Newsletter = () => (
  <form>
    <label>Email</label>
    <input type="text" />
    <button>Signup</button>
  </form>
);
```

Becomes:

```js
const Form = styled.form`...`;
const Label = styled.label`...`;
const Input = styled.input`...`;
const Button = styled.button`...`;
```

It was super easy to move components around.

## Composing styles

What I like about styled-components is how easy is to build blocks. You can also share styles between components with different primitives.

```js
import { fonts } from './ui';

const baseStyles = `
  font-family: ${fonts.sans};
  font-size: ${fonts.size}px;
`;

const BaseButton = styled.button`${baseStyles}`;
const BaseLink = styled.a`${baseStyles}`;

const StyledButton = styled(BaseButton)`
    padding: 0.25em;
    border: 0;
    outline: none;
`;

const StyledLink = styled(BaseLink)`
    color: ${colors.tomato};
    border-bottom: solid 3px currentColor;
`;
```

[Max](https://twitter.com/mxstbr) sent a note earlier which is worth mentioning:

When you define these reusable bits of styling always use the CSS helper because: a) you get syntax highlighting and b) you can use the `${props => x}` interpolations and they'll work for all the components you use that snippet in.

## Less dependencies

One less CSS file, everything in the same place. One less thing to setup in Webpack — in case you're not using [create-react-app](https://github.com/facebookincubator/create-react-app/).

## Real stylesheet

Styled-components [isn't the same thing as inline styles](http://mxstbr.blog/2016/11/inline-styles-vs-css-in-js/). It does generate the stylesheet with unique classes.

## Tooling support

Syntax highlight, auto-complete and lint support for [Atom](https://github.com/gandm/language-babel/blob/master/CHANGELOG.md#2520), [Visual Code](https://github.com/styled-components/vscode-styled-components) and [Sublime Text](https://github.com/styled-components/styled-components/issues/69).

<blockquote class="twitter-tweet" data-cards="hidden" data-lang="en"><p lang="en" dir="ltr">🔥 Autocompletion for CSS inside styled-components is now implemented in Atom!<a href="https://t.co/SLPSVbPmwg">https://t.co/SLPSVbPmwg</a> <a href="https://t.co/eo1gWfVByx">pic.twitter.com/eo1gWfVByx</a></p>&mdash; Max Stoiber (@mxstbr) <a href="https://twitter.com/mxstbr/status/826840687127752705">February 1, 2017</a></blockquote>

## Theming

Styled-components has [theming support](https://github.com/styled-components/styled-components#theming) out-of-the-box with `<ThemeProvider>`. I also use objects to define themes.

```js
const themes = {
  green: {
    bg: colors.green,
    fg: colors.white,
  },
  blue: {
    bg: colors.blue,
    fg: colors.white,
  }
};

const Link = styled.a`
  color: ${props => themes[props.theme].fg};
  background-color: ${props => themes[props.theme].bg};
`;

Link.defaultProps = {
  theme: 'blue',
};

// Usage: <Link theme="green" />
```

You can try different approaches and see which one works better.

## Helpers not mixins

You can port some of your Sass mixins to JavaScript. For example this function that does `px` to `em`.

```scss
@function em($px, $base: 16px) {
  @if unit($px) == "em" {
    @return $px;
  }
  @return ($px / $base) * 1em;
}
```

It can be writen in one line.

```js
// helpers.js
export const em = (px) => `${px / 16}em`;
```

```js
// text.js
import { em } from '../helpers';

const Text = styled.span`
  font-size: ${em(17)};
`;
```

Spoiler alert 👀: styled-components will ship a library containing all sorts of useful functions [soon](https://github.com/styled-components/styled-components/issues/482#issuecomment-279143316).


## Colors

If you're coming from a Sass background color functions `darken` or `lighten` are useful. The [color-js](https://www.npmjs.com/package/color) has a similar API inspired by Sass, Less and Stylus. I've been using [chroma-js](http://gka.github.io/chroma.js/).

```js
const darken = c => chroma(c).darken();

const Button = styled.div`
  color: ${props =>
      props.theme === 'darken' ?
        darken('mediumvioletred') :
        'mediumvioletred'
  };
  border-style: solid;
  border-width: 2px;
  border-color: currentColor;
`;
```

You can pick any other library to get advanced functionalies i.e. [bezier interpolation](gka.github.io/chroma.js/#chroma-bezier).

```js
const bezier = (colors) =>
  chroma
    .bezier(colors)
    .scale()
    .colors(5)
    .join(',');

const Box = styled.div`
  background-image:
    linear-gradient(
      15deg,
      ${props => bezier(props.colors) }
    );
`;
```

## Gotchas

Not really gotchas but I couldn't find a better title 😅. The things I found so far:

### Optional pseudo-class

Imagine you have a button with `hover` and `active` state but if the button is disabled you don't need them.

What I usually do is to keep the states in a `.active` class e.g.

```css
.root {
  background-color: lime;
}

.active {
  &:hover,
  &:active {
    background-color: saddlebrown;
  }
}
```

And bind the active class with `disabled` prop.

```js
const classNames = cx({
  [styles.active]: !disabled,
})
```

Simple and elegant solution. With styled-components you can write a function:

```js
function hover(disabled) {
  return disabled ?
    `` :
    `
     &:hover {
         background-color: saddlebrown;
     }
   `
}

const Button = styled.div`
  padding: 10px;
  background-color: lime;
  color: white;

  ${props => hover(props.disabled)}
`;
```

Because `styled()` receives a string you could concat them. Why not!?

```js
const base = `
  background-color: #ddd;
`;

const active = `
  &:hover {
    background-color: #666;
  }
`;

const Button = styled.div`${props =>
  props.disabled ? base : [base, active].join(' ')
}`;
```

Is this approach more complex? Definitely! Ugly? Probably 😅! At the same time it give us all the benefits of JavaScript. For me it's worth the trade-off.

### Custom components

You can use the `styled()` function to alter the returned component. This is also useful to filter props manually when you're dealing with third-party libraries.

```js
// heading.js
const fontSizes = {
  1: '52px',
  2: '48px',
  3: '40px',
}

const StyledHeading = styled(
  ({level, ...otherProps}) => {
    const Component = `h${level}`;
    return <Component {...otherProps} />
  }
)`
  font-size: ${props => fontSizes[props.level]};
`;

const Heading = ({level, children}) => (
  <StyledHeading level={level}>
    {children}
  </StyledHeading>
);
```

## What now

I love to write CSS. To simplify my workflow I slowly removed any pre-processor dependency when I started to build apps with JavaScript a few years ago.

> Styled-components made my workflow even simplier and boosted the DX 🚀

It's going to be hard to go back and write things in the traditional way.

## Further reading

- [Styled components 💅  —  Production Patterns](https://medium.com/@jamiedixon/styled-components-production-patterns-c22e24b1d896#.ehbtslz19)
- [Enforcing best practices in component-based systems](https://www.smashingmagazine.com/2017/01/styled-components-enforcing-best-practices-component-based-systems/)

---

Thanks to [@thekitze](https://twitter.com/thekitze), [@iamsapegin](https://twitter.com/iamsapegin) and [@mxstbr](https://twitter.com/mxstbr)
for the 🎩 tips.

Thanks to [@matteo_belfiore](https://twitter.com/matteo_belfiore) and [@FabioRuolo](https://twitter.com/FabioRuolo) to inspire me to write beautiful CSS everyday 😁
