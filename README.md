# Prismic + SvelteKit Porfolio Website

Project built with Prismic, SvelteKit with Typescript, Threejs, Tailwind css and Gsap.

&nbsp;

### Prismic

A headless content management system that has two Prismic packages installed:

- `@prismicio/client` provides helpers for fetching content from Prismic
- `@prismicio/svelte` provides Svelte components for rendering content from Prismic

There are two steps to rendering content from Prismic in this SvelteKit project:

1. Fetch content from the Prismic API using `@prismicio/client`.
2. Template the content using components from `@prismicio/svelte`.


### Slice Machine

This project includes an application called Slice Machine, which generates models for Custom Types and Slices. Slice Machine stores the models locally in the codebase, so it can save and version them. It also syncs the models to Prismic. To learn how to use Slice Machine, read [Model Content in SvelteKit](https://prismic.io/docs/content-modeling).

If you change or add to Custom Types, you'll need to update the route handling to match. To learn how to do that, read [Define Paths in SvelteKit](https://prismic.io/docs/technologies/define-paths-sveltekit).

## Documentation

For the official Prismic documentation, see [Prismic's guide for SvelteKit][prismic-docs] or the [technical references for the installed Prismic packages](https://prismic.io/docs/technologies/technical-references).

svelte
[sveltekit]: https://kit.svelte.dev/
[live-demo]: https://sveltekit-starter-prismic-minimal.vercel.app/
