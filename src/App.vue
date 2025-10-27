<template>
  <div class="page">
    <div>
      <h2>Vue 2.7 Deep-selectors (Colorful is working with LightningCSS) Demo</h2>
      <p><strong>Issue:</strong> LightningCSS warns about is not recognized as a valid pseudo-class.</p>
      <p><strong>Solution:</strong> Apply the same warning suppression from vite-plugin-vue to vite-plugin-vue2.</p>
      <p style="padding-left: 20px;">vite-plugin-vue: 📝 <a href="https://github.com/vitejs/vite-plugin-vue/issues/507#issuecomment-2608467665" target="_blank">Issue Discussion</a> • <a href="https://github.com/vitejs/vite-plugin-vue/pull/521" target="_blank">Proposed Fix</a></p>
      <div>
        <strong>Result:</strong>
        <ul>
          <li>
            <code>:deep()</code> and <code>::v-deep</code> work without warnings.
          </li>
          <li>
            Legacy <code>>>></code> and <code>/deep/</code> are not working, but can be replaced with <code>:deep()</code>.
          </li>
        </ul>
      </div>
    </div>
    <div class="square">
      <div class="one">:deep()</div>
      <div class="two">::v-deep</div>
      <div class="three">>>></div>
      <div class="four">/deep/</div>
    </div>
  </div>
</template>

<style scoped>
.page {
  height: 100vh;
  width: 100%;
  place-content: center;
  place-items: center;
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;

  h2 {
    margin-bottom: 10px;
    font-size: 1.5em;
  }

  p {
    margin: 8px 0;
    line-height: 1.6;
    font-size: 0.9em;

    code {
      background: #f4f4f4;
      padding: 2px 6px;
      border-radius: 4px;
      font-size: 0.85em;
    }

    a {
      color: #0066cc;
      text-decoration: none;

      &:hover {
        text-decoration: underline;
      }
    }
  }
  .square {
    display: flex;
    flex-direction: row;
    gap: 10px;
    margin-top: 20px;
    flex-wrap: wrap;

    & > div {
      width: 100px;
      height: 100px;
      padding: 10px;
      outline: 1px solid #0000001d;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 500;
    }
  }
  /* ============================================================
     Deep Selectors for Vue Scoped CSS
     Reference: https://vue-loader.vuejs.org/guide/scoped-css.html#deep-selectors
     stackoverflow: https://stackoverflow.com/questions/48032006/how-do-i-use-deep-or-or-v-deep-in-vue-js
     ============================================================ */

  /* ✅ WORKING: Vue 3 & Vue 2.7 - Recommended syntax */
  /* No LightningCSS warnings */
  & :deep(.one) {
    background-color: blue;
    color: white;
  }

  /* ✅ WORKING: Vue 2 (Sass syntax) */
  & ::v-deep .two {
    background-color: red;
    color: white;
  }

  /* ❌ BROKEN: Vue 2.0-2.6 non-Sass syntax */
  /* [lightningcss] Invalid dangling combinator in selector" */
  /* & >>> .three {
    background-color: green;
  } */

  /* ❌ BROKEN: Deprecated syntax */
  /* [lightningcss] Invalid dangling combinator in selector" */
  /* & /deep/ .four {
    background-color: yellow;
  } */
}
</style>
