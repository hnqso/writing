# Colors in Terminal

**Update 13/12/16** &mdash; I've added more context. Also more information on text styles and resource links at the bottom.

I built a little CLI tool [that-color](https://github.com/henriquea/that-color/) to name a color from a given hex. It also gives a nice color scale from [hello-color](https://github.com/jxnblk/hello-color). I use this tool often when I'm writing styleguide or mocking up components. I don't have to think about color names, values or open the browser.

<div class="image -fill">
  <img src="/assets/images/that-color.png" alt="that-color">
</div>

I started this project using the modules `colors`, `terminal-kit` and `ansy-styles`. The first time I used `ansi-styles` I got undefined trying to ouput the `style.color`. I looked into the code and from there I started a quick research around this subject.

Before write this library I didn't bother to understand how colors works in terminal. Just because this 👇 didn't look _friendly_.

```
printf "\u001b[38;2;230;90;180mhello world\u001b[0m"
```

It turned out to be more simple than I thought.

- `\u001B` unicode [ANSI escape code](en.wikipedia.org/wiki/ANSI_escape_code). By the way `\u001B`, `\x1b` and `\e` are different ways to write the same thing.
- `[` part of ANSI sequence escape.
- `38;`is the xterm-256 foreground color code. Use `48` to change the background color instead.
- `2;` is the color format code for 24-bit RGB [Truecolor](https://en.wikipedia.org/wiki/Color_depth#True_color_.2824-bit.29) ANSI support.
- `m` end of the sequence.
- `\u001b[0m` reset all changes for the next escape sequence.

Translating it to JavaScript make it easier to read and parse in my head:

```
`\u001B[${fg|bg};2;${r};${g};${b}m${msg}`
```

## Text style

The first parameter after `[` determines the style of the text. This value is off by default. Some of the attributes are: `0` for off, `1` for bold, `2` for underscore and `3` for blink.

Now the code looks like:

```
`\u001B[${style};${fg|bg};2;${r};${g};${b}m${msg}`
```

Not bad right!? You can use [supports-color](https://github.com/chalk/supports-color) to detect terminal color support. Now you're all set to build your own `colors.js` module or just use [ansy-styles](https://github.com/chalk/ansi-styles).

## Self note

Doing a bit of homework and trying to understand how things works under the hood is always self-rewarding.

## Resources

- [ANSI scape codes](https://en.wikipedia.org/wiki/ANSI_escape_code#CSI_codes)
- [Hello Color](http://jxnblk.com/hello-color/?c=07a845)
- [Color Hex](http://www.colorhexa.com/)
- [colors](https://www.npmjs.com/package/colors)
- [terminal-kit](https://www.npmjs.com/package/terminal-kit)
- [ansy-styles](https://github.com/chalk/ansi-styles)

{% assign url = page.url | prepend: site.url %}
<a href="https://twitter.com/intent/tweet?text={{page.title}}&url={{url}}&via=healves82" class="share">
  <i class="icon"><svg data-icon="twitter" viewBox="0 0 32 32" style="fill:currentcolor">
    <path d="M2 4 C6 8 10 12 15 11 A6 6 0 0 1 22 4 A6 6 0 0 1 26 6 A8 8 0 0 0 31 4 A8 8 0 0 1 28 8 A8 8 0 0 0 32 7 A8 8 0 0 1 28 11 A18 18 0 0 1 10 30 A18 18 0 0 1 0 27 A12 12 0 0 0 8 24 A8 8 0 0 1 3 20 A8 8 0 0 0 6 19.5 A8 8 0 0 1 0 12 A8 8 0 0 0 3 13 A8 8 0 0 1 2 4"></path>
  </svg></i> <span>Share this on Twitter</span>
</a>
