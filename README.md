# Vue 2 Deep Selectors issue with LightningCSS

This project demonstrates the issue and solution for LightningCSS warnings with Vue 2.7 deep selector syntax (`::v-deep`, `>>>`, `/deep/`) when using LightningCSS transformer.

## Problem

When using Vue 2.7 with LightningCSS (via `vite.config.ts`), the following warning appears:

```
[lightningcss] ** is not recognized as a valid pseudo-class selector
```

This occurs because LightningCSS doesn't recognize `::v-deep` as a valid pseudo-class, even though it's a valid Vue.js scoped CSS feature.

## Solution

Apply the same warning suppression mechanism from `vite-plugin-vue` to `vite-plugin-vue2`. The fix suppresses the specific warning about `v-deep` and `deep` pseudo-classes in LightningCSS.

### Patch Applied

This project uses `pnpm patch` to apply the fix. The patch is located in `patches/@vitejs__plugin-vue2@2.3.4.patch`.

### References

- [vite-plugin-vue Issue #507](https://github.com/vitejs/vite-plugin-vue/issues/507#issuecomment-2608467665)
- [vite-plugin-vue Pull Request #521](https://github.com/vitejs/vite-plugin-vue/pull/521)
- [Vue Deep Selectors Documentation](https://vue-loader.vuejs.org/guide/scoped-css.html#deep-selectors)
- [stackoverflow](https://stackoverflow.com/questions/48032006/how-do-i-use-deep-or-or-v-deep-in-vue-js)
## Deep Selector Syntax

- ✅ `:deep()` - Vue 3 & Vue 2.7 (Works without warnings with the patch)
- ✅ `::v-deep` - Vue 2.7 Sass syntax (Works without warnings with the patch)
- ❌ `>>>` - Legacy Vue 2 syntax (Broken with LightningCSS)
- ❌ `/deep/` - Deprecated syntax (Broken with LightningCSS)

## Usage

* not applied the patch
* remove the `pnpm.patchedDependencies` in package.json

```bash
# Install dependencies
pnpm i

# Start dev server
pnpm dev

# Build for production
pnpm build
```

* patch the plugin-vue2
* revert the `pnpm.patchedDependencies` in package.json

```bash
# Install dependencies
pnpm i

# Start dev server
pnpm dev

# Build for production
pnpm build
```
