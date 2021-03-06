# rangle-starter

[![Stories in Ready](https://badge.waffle.io/rangle/rangle-starter.png?label=ready&title=Ready)](https://waffle.io/rangle/rangle-starter) [![Join the chat at https://gitter.im/rangle/rangle-starter](https://badges.gitter.im/rangle/rangle-starter.svg)](https://gitter.im/rangle/rangle-starter?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

A command-line utility to create a repo based on one of Rangle.io's standard tech stacks.

These stacks are designed to play nice with Rangle.io's dev ops tools and
internal workflow. However they are open source and available to the community on an unsupported basis as well.

> [Looking for a tech stack that used to be here?](examples.md)

## Installation

Install it like this:

```
npm install -g rangle-starter
```

## Usage

First, create a repository for your new project on github. Leave it empty for
now.

Next, run `rangle-starter` and answer the questions in order to setup your new project.

This will create a new repo locally based on the appropriate tech stack.
`npm install; npm start` will build and run the sample app for that stack.

Push up your new repo with:

```sh
git push upstream master -u
```

Finally, go back to GitHub and fork your new repo to allow you to work using
Rangle-Flow (see note below).

## About the Stacks

JavaScript is evolving rapidly, with new approaches to application
development appearing almost on a monthly basis. As a training firm,
one of the services we provide is staying on top of these changes and
advising our clients on contemporary thinking.

On the other hand, as a consultancy, we also need to start up new
projects frequently and quickly, balancing up-to-date technology with
production-level expertise.

These stacks are what we use on our projects to get teams up and running
quickly, with our latest thinking on tools, technologies, and best
practices. However they are also provided, free of warranty, for community
usage under the terms of the MIT license.

Currently, we maintain starters for the following tech stacks:

* [Angular 2 with TypeScript](https://github.com/rangle/angular2-starter)
* [Angular 1 with TypeScript and Redux](https://github.com/rangle/angular-redux-starter)
* [API Koa Starter](https://github.com/rangle/api-koa-starter)

### React Starter

We transitioned to Facebook's Create-React-App project for building our react app starters.

* [Facebook's create-react-app](https://github.com/facebookincubator/create-react-app)
* [Rangle's react-scripts](https://www.npmjs.com/package/@rangle/react-scripts)

To build a react starter project use the following commands:

```
// Install
$ npm install create-react-app -g

// Use our @rangle/scripts with create-react-app to generate react/redux app
$ create-react-app my-starter-app --scripts-version @rangle/react-scripts
```

### Code Architecture

Regardless of framework, we favour an architectural approach based on
'atomic' components for presentation and Redux for state management. The
code layout and CSS toolchain have been carefully chosen to accomodate
this.

#### Component-Oriented Architecture (COA)

Component-oriented architecture is a way of thinking of apps as render
trees of simple, presentational components.  In this line of thinking,
we:

* build out a visual, domain-specific language of reusable UI components
* separate state management and business logic from these UI components as
much as we can.

Good presentational components have the following characteristics:
* They are very granular (even as little as a few lines of HTML)
* They encapsulate any CSS, HTML, and JS need to render themselves
* They are isolated and composable into larger page elements
* They are essentially pure functions that accept some attributes and
produce some DOM.

You can learn more about COA here:

* [Atomic Design blog post](http://bradfrost.com/blog/post/atomic-web-design/)
* [Intro to COA with Angular 2](https://www.youtube.com/watch?v=7cBaE_QwFWQ)

##### Presentational Components in React

For React, we use 'functional stateless components' to enforce these
concepts. Most of your components will be pure functions of their props
which return snippets of JSX.

Each component gets its own scoped CSS using the
`postss-local-by-default` transformation.

##### Presentational Components in Angular 2

In Angular 2, we use very granular `@Component` classes whose rendered
DOM is strictly a function of any `@Input` properties.

Each component gets its own scoped CSS using Angular 2's `ViewEncapsulation`
feature.

#### CSS Toolchain

An important aspect of COA is that components are responsible for their
own CSS. To means that we have to overcome the four classic problems
associated with CSS:

1. its global nature
2. its tendency to repeat large sets of rules across different classes
3. its inability to support dynamic features such as variables
4. enormously variable browser support.

We have chosen to address these using a toolchain based on OOCSS utility
classes and 'transpilation'.

##### OOCSS Utility Classes

Utility class libraries in CSS provide a large set of composable,
single-purpose classes that can be reference directly in your component
templates.  There are a few good ones, such as [tachyons](http://tachyons.io/) and
[basscss](http://www.basscss.com); our current favourite is basscss.

Basscss utilities end up taking care of the lion's share of styling for
our components.

##### CSS Transpilation

The other issues listed above are addressed using `postcss`, a 'transpiler'
for CSS. Postcss allows you to list a set of transformation plugins for your
CSS which can:

* allow `@import` and `variables` ([cssnext](http://cssnext.io/))
* handle vendor prefixing and known workarounds for you ([autoprefixer](https://autoprefixer.github.io/))
* scope CSS to a particular DOM or JSX element ([local-by-default](https://github.com/css-modules/postcss-modules-local-by-default)

This lets us write component-level CSS files that are properly scoped
and prefixed in the small number of cases where basscss is insufficient.

You can learn more about our CSS strategy from our
[Modular CSS training slides](http://rangle.github.io/intro-to-modular-css/).

### Developer Experience

We take developer experience very seriously. The starters are set up with
the following tools:

* source-map support for debugging the original transpiled code in the
browser
* named functional components for React dev tools (react starters only)
* full support for Augury, the [Angluar 2 Dev Tool Extension](https://augury.angular.io/)
* full support for the [Redux Devtools Chrome Extension](https://github.com/zalmoxisus/redux-devtools-extension)

Running any starter in dev mode will turn on these tools. Simply type
`npm run dev` and point your browser at http://localhost:8080.

### Building for Production

Of course, one of the main motivations of these starters is to have production
bundling set up and easy to go.

Typing `npm run build` will produce bundled, minified, JS and CSS for
optimal loading speed in most browsers.

Typing `npm start` will fire up a simple NodeJS server you can use to
serve your app; alternately you can deploy the contents of the `dist` folder
behind the HTTP server of your choice.

### Browser Support

We aim to support the same minimum browsers as the frameworks we use.
Currently that means Internet Explorer 9+ and the last two versions of
Chrome and Firefox.

### Quality Tools

Code quality is important to us. All our starters ship with unit testing
toolchains up and running.

We also use tslint and eslint for static code linting; and finally there
is a selenium-based E2E setup based on the Robot framework.

## A note on Rangle-flow

At Rangle.io we use a fork-and-branch strategy for pull requests, with some
modifications for our internal tooling.  Repos set up using this script assume
that your have a central repo for the team and developers work on personal forks.

Therefore the script sets up two remotes:

`origin`, which points to your personal fork, and `upstream`, which points to
a team repo which typically belongs your github organization.

If you want to change this, just fiddle with `git remote` after running the
script.

## More Info

For more in-depth discussion of these starters, see our

* [Blog Post](http://blog.rangle.io/real-world-javascript-standard-tech-stacks/)
* [React DevMonth Talk](https://www.youtube.com/watch?v=Sy4zy0NPcpo)
