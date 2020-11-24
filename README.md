# SVG Loader
SVGs from an external source can be rendered via `<img>` tags, but this has multiple drawbacks: you can't customize the fill, use CSS variables, or use focus/hover states.

SVG loader is a simple JS code you can include that fetches SVGs using XHR and injects the SVG code in the tag's place, giving you best of both worlds: externally stored SVGs (e.g, on CDN) and inline SVGs.

It's super-tiny: <1KB after gzipping and works well with frameworks.

[**Demo →**](https://jsfiddle.net/w9gz8kcv/)

## How to Use?
SVG Loader is designed to be plug and play. Hence, all you need to is to include the loader JS anywhere in your code, and then start using the code like this:

### Download and Include

```html
<!-- Include this code anywhere in your code -->
<script type="text/javascript" src="svg-loader.min.js" async></script>

<!-- Use an external SVG -->
<svg data-src="https://s.svgbox.net/loaders.svg?ic=spinner" width="50" height="50" fill="red"></svg>
<svg data-src="https://s.svgbox.net/loaders.svg?ic=spinner"
    width="50"
    height="50" 
    fill="currentColor"
    style="color: purple;"></svg>
```

**Note**: Because SVG Loader fetches file using XHRs, it's limited by CORS policies of the browser. 
So you need to ensure that correct `Access-Control-Allow-Origin` headers are sent with the file being served or that the files are hosted on your own domain. 


### Or, use from an npm package
The library is framework/platform agnostic. You should be able to use it in React, Vue.js and others
as long as you're inserting the correct attributes.


```
npm install external-svg-loader
```

Then, in your app, require/import `external-svg-loader` anywhere. Here's an example for create-react-app.

```jsx
import logo from './logo.svg';
import './App.css';
import 'external-svg-loader';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <svg
          data-src="https://s.svgbox.net/materialui.svg?ic=mail"
          width="50"
          fill="currentColor"
          style={{
            color: 'red'
          }}
        />
    </div>
  )
}
```

### Or, use a CDN
SVG loader can also be included via Cloudflare CDN. Example:

```html
<script type="text/javascript" src="https://unpkg.com/external-svg-loader@0.0.5/svg-loader.min.js" async></script>
```

## Disable/Modify Caching
By default, the XHR response is cached for 24 hours, so that any subsequent loads are instantenous. You can disable this behavior by passing `data-cache="disabled"`. You can also modify
the caching period by passing number of seconds. Example:

#### Cache for a week
```html
<svg data-src="https://s.svgbox.net/loaders.svg?ic=spinner" width="50" height="50" data-cache="604800"></svg>
```

#### Cache for a six hours
```html
<svg data-src="https://s.svgbox.net/loaders.svg?ic=spinner" width="50" height="50" data-cache="21600"></svg>
```

#### Disable Caching
```html
<svg data-src="https://s.svgbox.net/loaders.svg?ic=spinner" width="50" height="50" data-cache="disabled"></svg>
```

### Lazy Loading
You can also lazy load icons by using `data-loading=lazy`. This will make icon not load until it's about to enter the viewport. For lazy loading, `external-svg-loader` uses [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API).

```html
<svg data-src="https://s.svgbox.net/loaders.svg?ic=spinner" width="50" height="50" data-loading="lazy"></svg>
```

## LICENSE
MIT
