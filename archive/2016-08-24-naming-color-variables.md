# Naming Color Variables

It's always the same novel. We start a project with **one** color.

*Note: I'm using class names as example to make it more generic but it could be variables as well*

```
/* colors.css */
.grey {
  color: #eee;
}
```

Then one color become **two** or more.

```
/* colors.css */
.grey {
  color: #eee;
}

.grey-light {
  color: #f5f5f5;
}

.grey-darker {
  color: #9E9E9E;
}
```

Not a problem right? Well, now we need to add a fourth color something between `light` and `darker`. It's time to scratch your head and think about a good name because:

> Naming is hard

We found a name `grey-semi`. How about someone else looking at it without knowing the context? They will be like "Wuuuut!? grey-semi!?" What if we have more six colors?

<div class="image">
  <img src="https://i.imgflip.com/19h7g3.jpg" alt="Ain't nobody got time for that" />
</div>

Numbers for the rescue!

## Numeric values

When possible I like to use the same `font-weight` numeric values. Pick a number from `100` to `900`. Material design [color palette](https://material.google.com/style/color.html) does the same.

The primary `color` value starts at `400` or `500`. Lighter colors could start at `200` and darker at `700`. The idea is to have room to add colors in between but there is no rule.

```
/* colors.css */
.grey,
.grey-400 {
  color: #eee;
}

.grey-200 {
  color: #f5f5f5;
}

.grey-700 {
  color: #9E9E9E;
}
```

It's safe to guess that `grey-900` is darker than `grey-700`. The free bonus here is: we can stop worrying about naming colors.

{% assign url = page.url | prepend: site.url %}
<a href="https://twitter.com/intent/tweet?text={{page.title}}&url={{url}}&via=healves82" class="share">
  <i class="icon"><svg data-icon="twitter" viewBox="0 0 32 32" style="fill:currentcolor">
    <path d="M2 4 C6 8 10 12 15 11 A6 6 0 0 1 22 4 A6 6 0 0 1 26 6 A8 8 0 0 0 31 4 A8 8 0 0 1 28 8 A8 8 0 0 0 32 7 A8 8 0 0 1 28 11 A18 18 0 0 1 10 30 A18 18 0 0 1 0 27 A12 12 0 0 0 8 24 A8 8 0 0 1 3 20 A8 8 0 0 0 6 19.5 A8 8 0 0 1 0 12 A8 8 0 0 0 3 13 A8 8 0 0 1 2 4"></path>
  </svg></i> <span>Share this on Twitter</span>
</a>
