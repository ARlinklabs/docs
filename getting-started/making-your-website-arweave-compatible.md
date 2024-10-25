# Making Your Website Arweave Compatible

Learn how to prepare your web application for deployment on the Arweave permaweb. This guide covers essential modifications needed for different frameworks and explains important concepts for permaweb compatibility.

## Hash Routing Requirements

### Why Hash Routing?

When deploying applications to Arweave, hash routing is essential for several reasons:

1. **Serverless Architecture**
   * Arweave is a decentralized storage network without traditional servers
   * No server-side routing is available to handle clean URLs
   * Hash-based routing ensures all navigation happens client-side
2. **Data Permanence**
   * Content on Arweave is immutable once stored
   * Hash routing enables "dynamic" content within this immutable structure
   * Allows for SPA-like navigation without server intervention
3. **Performance Benefits**
   * All necessary code loads once at initial request
   * Reduces network requests during navigation
   * Improves overall application performance

{% hint style="warning" %}
Without hash routing, your application's routes may break when users refresh the page or share direct links.
{% endhint %}

## Framework-Specific Configuration

Choose your framework below for specific configuration instructions:

{% tabs %}
{% tab title="React" %}
#### ReactJS Configuration

1. Use HashRouter from react-router-dom:

```javascript
import { HashRouter } from 'react-router-dom';

function App() {
  return (
    <HashRouter>
      {/* Your routes here */}
    </HashRouter>
  );
}
```

2. Modify package.json:

```json
{
  "scripts": {
    "build": "PUBLIC_URL=./ react-scripts build"
  }
}
```
{% endtab %}

{% tab title="Next.js" %}
#### Next.js Configuration

1. Add to next.config.js:

```javascript
module.exports = {
  assetPrefix: "./",
  output: 'export',  // Enables static HTML export
  images: {
    unoptimized: true // Required for static export
  }
}
```

2. Update package.json:

```json
{
  "scripts": {
    "build": "next build && next export"
  }
}
```

{% hint style="info" %}
Next.js doesn't support hash routing. The manifest is adjusted for routes to work on reload, but dynamic routes may have limitations.
{% endhint %}
{% endtab %}

{% tab title="Vue" %}
#### Vue.js Configuration

1. Create or modify vue.config.js:

```javascript
module.exports = {
  publicPath: "./"
}
```

2. Use hash mode in router:

```javascript
import { createRouter, createWebHashHistory } from 'vue-router'

const router = createRouter({
  history: createWebHashHistory(),
  routes: [...]
})
```
{% endtab %}

{% tab title="Nuxt" %}
#### Nuxt.js Configuration

Modify nuxt.config.js:

```javascript
export default {
  target: 'static',
  router: {
    mode: 'hash',
    base: './'
  }
}
```
{% endtab %}

{% tab title="Vite" %}
#### Vite Configuration

1. Use hash router for your framework (React, Vue, or Svelte)
2. Update package.json:

```json
{
  "scripts": {
    "build": "vite build --base ./"
  }
}
```
{% endtab %}
{% endtabs %}

## File Path Requirements

### Using Relative Paths

All assets in your application must use relative paths because:

1. **Gateway Flexibility**
   * Your app can be accessed through different Arweave gateways
   * Absolute paths tied to specific domains won't work
   * Relative paths ensure resource accessibility regardless of gateway
2. **Decentralized Nature**
   * No central server or root directory exists
   * Files must be referenced relative to their location
   * Ensures assets are found regardless of access point

### Path Configuration Guidelines

{% hint style="info" %}
Follow these rules for proper path configuration:
{% endhint %}

1. **Asset References**
   * Use `./` prefix for same-directory resources
   * Use relative paths for images, styles, and scripts
   * Avoid absolute paths starting with `/`
2.  **Common Patterns**

    ```
    ✅ Good: ./images/logo.png
    ✅ Good: ../assets/style.css
    ❌ Bad: /images/logo.png
    ❌ Bad: https://mysite.com/images/logo.png
    ```
3. **Directory Navigation**
   * Same directory: `./file.jpg`
   * Child directory: `./images/file.jpg`
   * Parent directory: `../file.jpg`

## Deployment Checklist

Before deploying, verify these items:

* [ ] Hash routing implemented (if applicable)
* [ ] Build configuration updated for your framework
* [ ] All file paths are relative
* [ ] Assets are properly referenced
* [ ] Test build locally before deployment

{% hint style="info" %}
For HTML/CSS/JS applications without a framework, no special configuration is needed. You can deploy your files directly!
{% endhint %}

## Common Issues and Solutions

<details>

<summary>Broken images after deployment</summary>

* Check image paths are relative
* Verify image files are included in build
* Ensure correct case sensitivity in filenames

</details>

<details>

<summary>Routes not working on refresh</summary>

* Confirm hash routing is properly implemented
* Check router configuration
* Verify base URL configuration

</details>

<details>

<summary>Assets not loading</summary>

* Check for absolute paths in code
* Verify build configuration
* Ensure all assets are included in build directory

</details>

## Next Steps

Once your application is properly configured:

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Deploy Your App</strong></td><td>Learn how to deploy your configured application</td><td></td></tr><tr><td><strong>Testing</strong></td><td>Test your deployed application</td><td></td></tr><tr><td><strong>Troubleshooting</strong></td><td>Common issues and solutions</td><td></td></tr></tbody></table>
