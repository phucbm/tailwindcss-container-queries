> [!NOTE]
> As of Tailwind CSS v4.0, container queries are supported in the framework by default and this plugin is no longer required.

# @tailwindcss/container-queries

A plugin for Tailwind CSS v3.2+ that provides utilities for container queries.

## Installation

Install the plugin from npm:

```sh
npm install -D @phucbm/tailwindcss-container-queries
```

Then add the plugin to your `tailwind.config.js` file:

```js
// tailwind.config.js
module.exports = {
  theme: {
    // ...
  },
  plugins: [
    require('@phucbm/tailwindcss-container-queries'),
    // ...
  ],
}
```

## Usage

Start by marking an element as a container using the `@container` class, and then applying styles based on the size of that container using the container variants like `@md:`, `@lg:`, and `@xl:`:

```html
<div class="@container">
  <div class="@lg:underline">
    <!-- This text will be underlined when the container is larger than `32rem` -->
  </div>
</div>
```

By default we provide [container sizes](#configuration) from `@xs` (`20rem`) to `@7xl` (`80rem`).

### Named containers

You can optionally name containers using a `@container/{name}` class, and then include that name in the container variants using classes like `@lg/{name}:underline`:

```html
<div class="@container/main">
  <!-- ... -->
  <div class="@lg/main:underline">
    <!-- This text will be underlined when the "main" container is larger than `32rem` -->
  </div>
</div>
```

### Arbitrary container sizes

In addition to using one of the [container sizes](#configuration) provided by default, you can also create one-off sizes using any arbitrary value:

```html
<div class="@container">
  <div class="@[17.5rem]:underline">
    <!-- This text will be underlined when the container is larger than `17.5rem` -->
  </div>
</div>
```

### Removing a container

To stop an element from acting as a container, use the `@container-normal` class.

<div class="@container xl:@container-normal">
  <!-- ... -->
</div>

### With a prefix

If you have configured Tailwind to use a prefix, make sure to prefix both the `@container` class and any classes where you are using a container query modifier:

```html
<div class="tw-@container">
  <!-- ... -->
  <div class="@lg:tw-underline">
    <!-- ... -->
  </div>
</div>
```

## Configuration

By default we ship with the following configured values:

| Name   | CSS                                          |
| ------ | -------------------------------------------- |
| `@xs`  | `@container (min-width: 20rem /* 320px */)`  |
| `@sm`  | `@container (min-width: 24rem /* 384px */)`  |
| `@md`  | `@container (min-width: 28rem /* 448px */)`  |
| `@lg`  | `@container (min-width: 32rem /* 512px */)`  |
| `@xl`  | `@container (min-width: 36rem /* 576px */)`  |
| `@2xl` | `@container (min-width: 42rem /* 672px */)`  |
| `@3xl` | `@container (min-width: 48rem /* 768px */)`  |
| `@4xl` | `@container (min-width: 56rem /* 896px */)`  |
| `@5xl` | `@container (min-width: 64rem /* 1024px */)` |
| `@6xl` | `@container (min-width: 72rem /* 1152px */)` |
| `@7xl` | `@container (min-width: 80rem /* 1280px */)` |

You can configure which values are available for this plugin under the `containers` key in your `tailwind.config.js` file:

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      containers: {
        // Min-width container queries (default)
        '2xs': '16rem',

        // Max-width container queries (new)
        'mobile': { max: '30rem' },   // @mobile applies when container width ≤ 30rem (480px)
        'tablet': { max: '48rem' },   // @tablet applies when container width ≤ 48rem (768px)

        // You can also explicitly define min-width using the object syntax
        'desktop': { min: '64rem' },  // Same as: 'desktop': '64rem'
      },
    },
  },
}
```

### Container Query Types

The configuration API is inspired by Tailwind's `screens` configuration, using the same syntax and structure.

#### Min-width Queries (Default)
When using a string value, the plugin creates a min-width container query:

```js
containers: {
  'sm': '24rem'  // Creates: @container (min-width: 24rem)
}
```

#### Max-width Queries
To create max-width container queries, use an object with the `max` property:

```js
containers: {
  'mobile': { max: '30rem' }  // Creates: @container (max-width: 30rem)
}
```

This allows you to apply styles when a container is smaller than a specified width, which is useful for mobile-first approaches or adapting layouts for smaller container contexts.

The object syntax matches how you would configure responsive breakpoints in Tailwind's `screens` option, making it familiar and consistent with the rest of your Tailwind configuration.