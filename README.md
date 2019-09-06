# gatsby-plugin-react-svg-loader [![npm version](https://badge.fury.io/js/gatsby-plugin-react-svg-loader.svg)]

[gatsby-plugin-react-svg](https://github.com/jacobmischka/gatsby-plugin-react-svg) equivalent but using `@svgr/webpack` instead.

Adds [`@svgr/webpack`](https://github.com/smooth-code/svgr) to gatsby webpack config.

> **Note**: the plugin can **remove `SVG`s from the built-in `url-loader` config** in case invalid configuration.

## Install

`npm install --save gatsby-plugin-react-svg-loader`

## How to use

```js
// In your gatsby-config.js

plugins: [
  {
    resolve: "gatsby-plugin-react-svg-loader",
    options: {
      rule: {
        include: /assets/ // See below to configure properly
      }
    }
  }
];
```

## Configuration

The `rule` plugin option can be used to pass [rule options](https://webpack.js.org/configuration/module/#rule). If either `include` or `exclude` options are present, `@svgr/webpack` will use them and `url-loader` will be re-enabled with the inverse.

The following configuration uses `@svgr/webpack` to process SVGs from a path matching `/assets/`, and `url-loader` to process SVGs from everywhere else.

```js
{
    resolve: 'gatsby-plugin-react-svg-loader',
    options: {
        rule: {
          include: /assets/
        }
    }
}
```

From now on you can import SVGs and use them as Components:

```js
import Icon from "./path/assets/icon.svg";

// ...

<Icon />;
```

Another common configuration:

- name SVGs used in React components like `something.inline.svg` and process them with `@svgr/webpack`
- name other SVGs (e.g. used in css/scss) `something.svg` and process them with the default `url-loader`

```js
{
    resolve: 'gatsby-plugin-react-svg-loader',
    options: {
        rule: {
          include: /\.inline\.svg$/
        }
    }
}
```

In React components:

```js
import Something from "./path/something.inline.svg";

// ...

<Something />;
```

In styles file:

```css
.header-background {
  background-image: url(./path/something.svg);
}
```