# Before dive into React

I’m helping a few friends to get started with React but only the fundamentals. They don’t have any previous experience with front-end development.

If you're already a front-end developer you may skip to [What to learn in 2017 if you’re a frontend developer](https://medium.com/@sapegin/what-to-learn-in-2017-if-youre-a-frontend-developer-b6cfef46effd#.epqapplk0).

## Asking the right question

How to make the right questions, when to ask them and what not to ask is important. Let's say you're not sure how to manage states and Google [react state management](https://www.google.co.uk/search?q=react+manage+state). You can easily land on a post about stores and redux. This is going to make your head spin and overheat your brain.

In almost every conversation I tell them the follow:

> Stop googling and reading everything about React.

The web is full of noise and outdated information as well. It’s easy to end up in the wrong place. Some of the tutorials may tell you how to setup Webpack. Nothing wrong here but you don't need this information just yet.

> Start from the basics. There are no shortcuts.

Some of the questions are not related with React at all. They're classic JavaScript questions. Avoid shortcuts. They may look harmless
in the beginning. In the medium and long run they confuse and scramble important concepts.

In all cases they asked about Redux.

> No. You don’t need Redux, React Router, CSS Modules, Webpack or anything else to learn React.

At this point I already asked them to stop what they are doing and get back to the first base.

## Getting familiar

If you're **not** coming from a front-end development background you should get the basics. The subject becomes familiar and you know how to ask for directions.

> Focus on the key concepts not details.

Mozilla Developer Network or [MDN](https://developer.mozilla.org/en-US/) is a good place to start. I use it as main place to check any spec documentation about HTML, CSS or JavaScript.

### Web and Browser

- HTTP requests
- Browser rendering &mdash; the [pixel pipeline](https://developers.google.com/web/fundamentals/performance/rendering/) graph

### CSS

- CSS naming conventions like [BEM](http://getbem.com/naming/) and [Suit](https://suitcss.github.io/)
- [Layout with Flexbox](http://cssreference.io)
- [Good practices](https://github.com/airbnb/css)

### JavaScript

- [What is JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Introduction)
- [The basics](http://speakingjs.com/es5/ch01.html)
- [Style guide](https://github.com/airbnb/javascript)
- ES6/ES2015

### Bundlers

- [What is a module bundler](https://medium.com/@gimenete/how-javascript-bundlers-work-1fc0d0caf2da#.5q92kxunk)
- [Webpack](https://webpack.js.org/), [Browserfy](http://browserify.org/) and [Rollup](http://rollupjs.org/)

### Tooling

- [Babel](https://babeljs.io)
- [npm](https://www.npmjs.com/) and [yarn](https://yarnpkg.com/)
- [Chrome DevTools](https://developer.chrome.com/devtools)
- Basic terminal operations `ls`, `cp`, `mv`, `mkdir`, etc
- Check out [iTerm](https://www.iterm2.com/version3.html) and [Hyper](https://hyper.is/) terminals
- Use [JS Bin](http://jsbin.com/?html,css,js,output), [WebpackBin](http://www.webpackbin.com/) or [CodePen](http://codepen.io/) for quick prototyping
- [Atom](https://atom.io/), [Code](https://code.visualstudio.com/), [Sublime Text](https://www.sublimetext.com/3)

### Git and GitHub

- [Git flow](https://guides.github.com/introduction/flow/)
- Create repositories on GitHub
- [What is a pull request](https://help.github.com/articles/about-pull-requests/)
- Clone a project from GitHub in your terminal with `git clone`
- Pull, commit and push changes

### Component design

- [Design systems](http://danielmall.com/articles/researching-design-systems/)
- [Atomic design](http://bradfrost.com/blog/post/atomic-web-design/)
- [Content and display patterns](http://danielmall.com/articles/content-display-patterns/)
- [Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html)

Don't get intimidated by this list.

> Read. Experiment. Fail. Repeat. Keep going until you get it right.

It's a solid foundation not only to learn React but any other web technology.

If there is anything else that should be in this list please ping me on Twitter.

{% assign url = page.url | prepend: site.url %}
<a href="https://twitter.com/intent/tweet?text={{page.title}}&url={{url}}&via=healves82" class="share">
  <i class="icon"><svg data-icon="twitter" viewBox="0 0 32 32" style="fill:currentcolor">
    <path d="M2 4 C6 8 10 12 15 11 A6 6 0 0 1 22 4 A6 6 0 0 1 26 6 A8 8 0 0 0 31 4 A8 8 0 0 1 28 8 A8 8 0 0 0 32 7 A8 8 0 0 1 28 11 A18 18 0 0 1 10 30 A18 18 0 0 1 0 27 A12 12 0 0 0 8 24 A8 8 0 0 1 3 20 A8 8 0 0 0 6 19.5 A8 8 0 0 1 0 12 A8 8 0 0 0 3 13 A8 8 0 0 1 2 4"></path>
  </svg></i> <span>Share this on Twitter</span>
</a>
