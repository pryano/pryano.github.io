## Tailwind CSS

I recently decided to experiment with Svelte and Sveltekit, but had to
reorient myself on the current styling ecosystem. You no longer have to worry
so much about manually adding fixes for each browser, but there are new 
challenges to address.
1. Utility vs Class-based styling
2. Style modifiers
3. Flex vs Grid layouts
4. Dark-mode themes
5. Dynamic style changes
6. CSS pruning

### Utility Classes
TailWindCSS uses utility-class styling. This means that we have a set of class names
that describe a style, and components are modified with whatever style names we
want to apply to the component. So we end up with something like this:
```html
<div class="grid place-items-center gap-5 rounded-lg bg-green-300"> 
```

This is an alternative to class-based styles where you have a component name
as the class, and then the actual styling is defined in the css definition, like
this:
```html
<div class="main-card-display">
```
```css
.main-card-display {
  # grid styling
  # background color
  # rounding
  # centering
}
```

What I like about utility classes is that we know what we're getting
when we look at the component, we don't need to reference another file
or css style block. Another benefit is that there is no hidden meaning
in the class names. What you see is what you get.

One drawback to utility classes is that it's not DRY, so when we
want to modify all rounded divs to have sharp edges instead, we must
search+replace instead of editing a single `my-pretty-div` css class. On
the other hand, search+replace is not hard since the style names are static. And
with modern component-based development, we should already have some degree of DRYness
in our code to help limit the scope of a change.

### Style modifiers
TailwindCSS comes out of the box with pseudo-classes, elements, media queries, 
and attribute selectors. To define a hover styling, just add the `hover:` prefix like so:
```html
<div class="rounded-lg hover:rounded-sm bg-green-300 hover:bg-blue-300">
```
Keeping with the theme of readable styling, the hover styling stays on the
component it is modifying. We don't need to reference any other code.

### Flex vs Grid Layouts
TailwindCSS gives full control over both grid and flex based layouts, with
excellent documentation for both. It also provides sensible options for centering,
alignment, gaps, and stretching.

### Dark mode theme
Dark/Light mode theme options are becoming more important as we look for ways
to read our phones in movie theaters without bothering those around us.
TailwindCSS offers a `dark:` prefix option to styles and the ability to
define the dark-mode versions of classes for more customization. The `dark:` versions of styles need to be included
alongside the regular styles, so again we can know what we're going to get
just by looking at the class names. So we see code like this:
```html
<div class="rounded-lg bg-green-300 dark:bg-green-50">
```

### Dynamic Style Changes
Sometimes we want a style to be user-driven or otherwise dynamic. Maybe we
have a conditional class -- if the `player-card` is `activated`, give it a 
blue border, otherwise black. This is where I have found the main pain-points
of tailwindcss. Tailwind compiles the minimum set of css required for our project,
and it does this by doing a 'dumb' regex search of our code looking for its
class names. Anything it doesn't find gets trimmed from the final package. It
doesn't interpet our code to determine all possible classes. This means 
we need to have the full style names `somewhere` in the code, via code comments or:
```html
<div class={ isActive ? "bg-blue-300" : "bg-slate-300"}>
```

Not
```html
<div class="bg-{color}-300">
```
We could also modify the config to always include certain styles, but that bloats
all our static pages (depending on your customization, it could be trivial).

Its a bit annoying, but it mostly works. As long as style sets are manageable. And
as long as the style is not truly dynamic or user-provided. If we want the
user to be able to provide their own RGB color for an element, we must break out
of tailwind and add the style programmatically.

### CSS Pruning
As described above, TailwindCSS prunes the styles to only what's used in our code.
This is great for static content, as it keeps the style sheets pretty small.

## Over Verdict
I'll keep using TailwindCSS whenever possible, as the utility classes and excellent
documentation take most of the pain out of styling and allow me to focus on _what style
do I want_ instead of _how do I apply the style I want_.
