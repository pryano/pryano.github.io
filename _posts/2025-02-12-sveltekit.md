# Svelte and SvelteKit
A little over a year ago I came across Svelte and immediately loved the component-oriented approach to encapsulation. 
I went through the tutorials, checked the docs, and then decided to test the waters by building a simple Single Page App.
After tinkering with it and uncovering several warts, I set it aside and decided to give it a little more
time to mature before diving back in. And with the latest v2 release, most of those warts have gone away and
I'm excited to give it another spin!

tldr; I'm loving it!

## Routes
While we can use Svelte on the frontend and plug it into another framework for serving pages and data, 
I decided to go all in with SvelteKit on the backend (running on node) so I could get a feel for the routing and state management. 
And it really clicked with me! 

The convention of using the directory structure to define the routes eliminates one of the
biggest problems we run into with documentation -- drift! Ideally, documentation is driven by the code, so there's not a
disconnect from the source of truth and we don't have to remember to update the docs when the code changes.
SvelteKit's routes are very clear sources of truth, so we don't need to hunt for mappings of route->handler, it's
right there in the folder heirarchy! On top of that, routes also let us define strongly typed parameters and easily digestable APIs!

## Reactivity
Pretty much every modern framework is built around reactivity, where components "react" to changes to the
underlying data. SvelteKit is no different, with component props and state management helpers. Prior to SvelteKit v2, 
there was some ugly magic that you had to memorize to keep data reactive, but with the newer release that
magic has been replaced with more intuitive function calls. I'll touch on that in a later post.

Between passing props to components, binding to props, defining derived state, and handling state, I've
been very happy with the built-in tools for handling data.

## Page Data
SvelteKit also provides a pretty straightforward way to handle server-side functionality like form actions,
API endpoints (leaning towards restful GET/POST/etc handlers), and passing data from the server to the 
clients. The documentation really pushes for the use of server FormActions, which are the right tool for many
situations, but when we need to fall back to regular POST handlers, we have that option too.

## Layouts
Aside from defining pages, SvelteKit also lets us define layouts that apply to all child pages. This makes
it a breeze to add a navbar, or sidebar for all admin pages, or shopping bar for all shopping pages, or ...
you get the idea. That shared logic and presentation is very easy to encapsulate.

## Frontendery
A really nice thing has been the built-in support for transitions, animations, each blocks, etc, just generally
making the frontend development enjoyable! Setting up the styling is very easy with the way plugins work with svelte and vite. For example, getting Tailwindcss and DaisyUI working took all of 2 minutes -- quick and painless!
