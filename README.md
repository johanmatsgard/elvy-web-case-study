# elvyenergy.com

Elvy's marketing website. The code lives in a private company repo, so this is a write-up of how it's built. The design system itself is public: [elvyenergy.com/design-system](https://www.elvyenergy.com/design-system)

## From Figma to code

I started in Figma, first with the design system and then with mockups of the site built from it. That system was then translated into code as tokens (colors, type, spacing, radii, shadows) and components that pull from them, each with enough parameters that new pages can be put together without new styling.

## Styling is never invented

All tokens live in one file. A script turns them into the Tailwind theme, and the generated CSS is committed but never edited by hand. Components can only use token-backed classes, and a custom lint rule blocks arbitrary values, so nobody, person or model, can slip in a one-off color or margin.

The design system page on the live site renders the actual components, so the documentation always matches production.

## No CMS

There's no admin panel. Content is edited by talking to an AI coding agent (I use Claude Code): you describe the change and drop in any images, and it edits the right file, uploads the images and opens a pull request with a preview link. Nothing goes live on its own. Once the preview has been reviewed and the checks pass, content changes ship automatically, usually within minutes.

Since the site is plain code with strict rules, it isn't tied to one tool. When a better model comes out, it can start working on the site right away.

## Checks

Every change goes through one gate: formatting, linting (including the design-system rule), type checking, tests, and a check that generated files haven't drifted from the tokens. There are also accessibility checks for contrast and document structure.

## Also in there

- Swedish and English versions of every page
- An onboarding flow with Swedish address autocomplete that can look up details about the house, so customers don't have to type them in
- Transactional emails built with React Email

Stack: Next.js (App Router), React 19, TypeScript, Tailwind v4, next-intl, Vercel.
