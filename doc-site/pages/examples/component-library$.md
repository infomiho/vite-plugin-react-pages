---
title: Examples
group: /
order: 4
subGroup: advanced
---

# Example: develop a component library

This is an example of using "Advanced Filesystem Routing" inside a component library project.

Suppose you are developing a React component library. Your project will have a file structure like this:

```text
src
├── Button
│   ├── demos
│   │   ├── demo1.tsx
│   │   └── demo2.tsx
│   ├── index.tsx
│   ├── style.module.css
│   └── README.md
├── Card
│   ├── demos
│   │   ├── demo1.tsx
│   │   └── demo2.tsx
│   ├── index.tsx
│   ├── style.module.css
│   └── README.md
└── index.ts
```

You want to use Vite as your local demo development environment (because it is blazingly fast). **How to collect all components and all demos from this project?** The file structure doesn't follow the [Basic Filesystem Routing Convention](/fs-routing).

The answer: implement your own filesystem routing convention!

vite.config.ts:
<FileText src="../../../packages/create-project/template-lib/docs/vite.config.ts" syntax="ts" />

We use `api.getRuntimeData(pageId)` and `api.getStaticData(pageId)` inside fileHandlers to get the pageData object. We can mutate the data object, and vite-pages will update its pages accordingly.

Check out the complete example in [the library project scaffold](https://github.com/vitejs/vite-plugin-react-pages/blob/main/packages/create-project/template-lib/docs/vite.config.ts).
You can initialize this project [with one command](/) (choose `lib` template).

## Monorepo

In some cases, we want to publish each component in their own packages.

> Monorepo has more advantages when components are complex and tend to evolve independently. If we use a single package to publish all these components like the above example, all components share a version number. If we need to introduce a breaking change in a component, we have to bump the major version of the whole package. But with the monorepo we only need to bump the major version of that sub-package. Users will be more confident to upgrade.

In that case, we create a separate package to run vite-pages, collecting all components and their demos. The project setup will look like this:

```text
packages
├── Button
│   ├── demos
│   │   ├── demo1.tsx
│   │   └── demo2.tsx
│   ├── src
│   │   ├── index.tsx
│   │   └── style.module.css
│   ├── package.json
│   └── README.md
├── Card
│   ├── demos
│   │   ├── demo1.tsx
│   │   └── demo2.tsx
│   ├── src
│   │   ├── index.tsx
│   │   └── style.module.css
│   ├── package.json
│   └── README.md
├── demos
│   ├── pages
│   │   ├── index$.tsx
│   │   └── _theme.tsx
│   ├── index.html
│   ├── package.json
│   └── vite.config.ts
└── package.json
```

Check out the complete example in [the lib-monorepo scaffold](https://github.com/vitejs/vite-plugin-react-pages/blob/main/packages/create-project/template-lib-monorepo/packages/demos/vite.config.ts).
You can initialize this project [with one command](/) (choose `lib-monorepo` template).
