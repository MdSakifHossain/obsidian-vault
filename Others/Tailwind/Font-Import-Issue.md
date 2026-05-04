# Font Import Issue

⬅️ [Tailwind](Tailwind.md)

I'm so fucking stupid. 😒😒

## Issue

```shell
$ npm run dev

> the_frontend_part@0.0.0 dev
> vite


  VITE v7.2.7  ready in 183 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
[vite:css][postcss] @import must precede all other statements (besides @charset or empty @layer)
2636 |    unicode-range: U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+0304,U+0308,U+0329,U+2000-206F,U+2...
2637 |  }
2638 |  @import url("https://fonts.googleapis.com/css2?family=Libre+Barcode+128+Text&family=Outfit:wght@100..900&family=Press...
     |  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
2639 |  :root {
2640 |    --background: oklch(1 0 0);

```

This issue has happened because i have imported the `Google Font` in the `inde.css` file. Well, this could happend if I import font from any `webfont embedding service`.

## Explanation

```
@import "tailwindcss";
@import "tw-animate-css";
@import "shadcn/tailwind.css";
@import "@fontsource-variable/jetbrains-mono";

@import url("https://fonts.googleapis.com/css2?family=Libre+Barcode+128+Text&family=Outfit:wght@100..900&family=Press+Start+2P&display=swap");
@theme {
  --font-pixel: "Press Start 2P", system-ui;
  --font-outfit: "Outfit", sans-serif;
  --font-barcode: "Libre Barcode 128 Text", system-ui;
}

@custom-variant dark (&:is(.dark *));

/* And, rest of the code... */
```

_**Everying is just fine except for the `line 6`. It's just one the wrong place.**_

## Solution

We just have to move the line from `line 6` to `line 1`. And, **Everything else after that.**

```
@import url("https://fonts.googleapis.com/css2?family=Libre+Barcode+128+Text&family=Outfit:wght@100..900&family=Press+Start+2P&display=swap");
@import "tailwindcss";
@import "tw-animate-css";
@import "shadcn/tailwind.css";
@import "@fontsource-variable/jetbrains-mono";

@theme {
  --font-pixel: "Press Start 2P", system-ui;
  --font-outfit: "Outfit", sans-serif;
  --font-barcode: "Libre Barcode 128 Text", system-ui;
}

@custom-variant dark (&:is(.dark *));

/* And, rest of the code... */
```

## Note

> So, I have to put the imported font on top of the css file and the rest of the shit afterwards

## Reference

Well, I don't have any reference on this topic. Just added this topic so that the page would be a little longer. 😁
