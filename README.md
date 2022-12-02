# techno-vue-treeselect
[![npm](https://badgen.now.sh/npm/v/@riophae/vue-treeselect)](https://www.npmjs.com/package/@riophae/vue-treeselect) [![Build](https://badgen.now.sh/circleci/github/riophae/vue-treeselect)](https://circleci.com/gh/riophae/vue-treeselect/tree/master) [![Coverage](https://badgen.net/codecov/c/github/riophae/vue-treeselect)](https://codecov.io/gh/riophae/vue-treeselect?branch=master)
![npm monthly downloads](https://badgen.now.sh/npm/dm/@riophae/vue-treeselect)
![jsDelivr monthly hits](https://badgen.net/jsdelivr/hits/npm/@riophae/vue-treeselect) [![Known vulnerabilities](https://snyk.io/test/npm/@riophae/vue-treeselect/badge.svg)](https://snyk.io/test/npm/@riophae/vue-treeselect) ![License](https://badgen.net/github/license/riophae/vue-treeselect)

> A multi-select component with nested options support for Vue.js

![Vue-Treeselect Screenshot](https://raw.githubusercontent.com/riophae/vue-treeselect/master/screenshot.png)

### Features

- Single & multiple select with nested options support
- Fuzzy matching
- Async searching
- Delayed loading (load data of deep level options only when needed)
- Keyboard support (navigate using <kbd>Arrow Up</kbd> & <kbd>Arrow Down</kbd> keys, select option using <kbd>Enter</kbd> key, etc.)
- Rich options & highly customizable
- Supports a wide range of browsers (see [below](#browser-compatibility))
- RTL support

*Requires Vue 2.2+*

### Getting Started

It's recommended to install vue-treeselect via npm, and build your app using a bundler like [webpack](https://webpack.js.org/).

```bash
npm install @mail2gowthamganesan/techno-vue-treeselect
```

This example shows how to integrate vue-treeselect with your [Vue SFCs](https://vuejs.org/v2/guide/single-file-components.html).

```vue
<!-- Vue SFC -->
<template>
  <div id="app">
    <treeselect v-model="value" :multiple="true" :options="options" />
  </div>
</template>

<script>
  // import the component
  import Treeselect from '@mail2gowthamganesan/vue-treeselect'
  // import the styles
  import '@mail2gowthamganesan/vue-treeselect/dist/vue-treeselect.css'

  export default {
    // register the component
    components: { Treeselect },
    data() {
      return {
        // define the default value
        value: null,
        // define options
        options: [ {
          id: 'a',
          label: 'a',
          // control checkbox show/hide
          checkBox: false,
          children: [ {
            id: 'aa',
            label: 'aa',
          }, {
            id: 'ab',
            label: 'ab',
          } ],
        }, {
          id: 'b',
          label: 'b',
        }, {
          id: 'c',
          label: 'c',
        } ],
      }
    },
  }
</script>
```

## Props

| Name | Type / Default | Description |
| --- | --- | --- |
| **allowClearingDisabled** | **Type:** Boolean  **Default:** `false` | Whether to allow resetting value even if there are disabled selected nodes. |
| **allowSelectingDisabledDescendants** | **Type:** Boolean **Default:** `false` | When an ancestor node is selected/deselected, whether its disabled descendants should be selected/deselected. You may want to use this in conjunction with `allowClearingDisabled` prop. |
| **alwaysOpen** | **Type:** Boolean **Default:** `false` | Whether the menu should be always open. |
| **appendToBody** | **Type:** Boolean **Default:** `false` | Append the menu to `<body />`. |
| **async** | **Type:** Boolean **Default:** `false` | Whether to enable [async search mode](#async-searching). |
| **autoFocus** | **Type:** Boolean **Default:** `false` | Automatically focus the component on mount. |
| **autoLoadRootOptions** | **Type:** Boolean **Default:** `true` | Automatically load root options on mount. When set to `false`, root options will be loaded when the menu is opened. |
| **autoDeselectAncestors** | **Type:** Boolean **Default:** `false` | When user deselects a node, automatically deselect its ancestors. Applies to flat mode only. |
| **autoDeselectDescendants** | **Type:** Boolean **Default:** `false` | When user deselects a node, automatically deselect its descendants. Applies to flat mode only. |
| **autoSelectAncestors** | **Type:** Boolean **Default:** `false` | When user selects a node, automatically select its ancestors. Applies to flat mode only. |
| **autoSelectDescendants** | **Type:** Boolean **Default:** `false` | When user selects a node, automatically select its descendants. Applies to flat mode only. |
| **backspaceRemoves** | **Type:** Boolean **Default:** `true` | Whether <kbd>Backspace</kbd> removes the last item if there is no text input. |
| **beforeClearAll** | **Type:** Fn() 🡒 (Boolean \| Promise<Boolean>) **Default:** `() => true` | Function that processes before clearing all input fields. Return `false` to stop values being cleared. |
| **branchNodesFirst** | **Type:** Boolean **Default:** `false` | Show branch nodes before leaf nodes. |
| **cacheOptions** | **Type:** Boolean **Default:** `true` | Whether to cache results of each search request for [async search mode](#async-searching). |
| **clearable** | **Type:** Boolean **Default:** `true` | Whether to show an "×" button that resets value. |
| **clearAllText** | **Type:** String **Default:**`"Clear all"` | Title for the "×" button when `:multiple="true"`. |
| **clearOnSelect** | **Type:** Boolean **Default:** Defaults to `false`when `:multiple="true"`; always `true`otherwise. | Whether to clear the search input after selecting an option. Use only when `:multiple="true"`. For single-select mode, it **always** clears the input after selecting regardless of the prop value. |
| **clearValueText** | **Type:** String **Default:**`"Clear value"` | Title for the "×" button. |
| **closeOnSelect** | **Type:** Boolean **Default:** `true` | Whether to close the menu after selecting an option. Use only when `:multiple="true"`. |
| **defaultExpandLevel** | **Type:** Number **Default:** `0` | How many levels of branch nodes should be automatically expanded when loaded. Set `Infinity` to make all branch nodes expanded by default. |
| **defaultOptions** | **Type:** Boolean |`node[]` **Default:** `false` | The default set of options to show before the user starts searching. Used for [async search mode](#async-searching). When set to `true`, the results for search query as a empty string will be autoloaded. |
| **deleteRemoves** | **Type:** Boolean **Default:** `true` | Whether <kbd>Delete</kbd> removes the last item if there is no text input. |
| **delimiter** | **Type:** String **Default:**`","` | Delimiter to use to join multiple values for the hidden field value. |
| **flattenSearchResults** | **Type:** Boolean **Default:** `false` | Whether to flatten the tree when searching (sync search mode only). See [here](#flatten-search-results) for example. |
| **disableBranchNodes** | **Type:** Boolean **Default:** `false` | Whether to prevent branch nodes from being selected. See [here](#disable-branch-nodes) for example. |
| **disabled** | **Type:** Boolean **Default:** `false` | Whether to disable the control or not. |
| **disableFuzzyMatching** | **Type:** Boolean **Default:** `false` | Set to `true` to disable the fuzzy matching functionality, which is enabled by default. |
| **flat** | **Type:** Boolean **Default:** `false` | Whether to enable flat mode or not. See [here](#flat-mode-and-sort-values) for detailed information. |
| **instanceId** | **Type:** String | Number **Default:** `"<auto-incrementing number>$$"` | Will be passed with all events as the last param. Useful for identifying events origin. |
| **joinValues** | **Type:** Boolean **Default:** `false` | Joins multiple values into a single form field with the `delimiter` (legacy mode). |
| **limit** | **Type:** Number **Default:** `Infinity` | Limit the display of selected options. The rest will be hidden within the `limitText` string. |
| **limitText** | **Type:** Fn(`count`) 🡒 String **Default:** ``count => `and ${count} more``` | Function that processes the message shown when selected elements pass the defined limit. |
| **loadingText** | **Type:** String **Default:** `"Loading..."` | Text displayed when loading options. |
| **loadOptions** | **Type:** Fn({`action`, `callback`, `parentNode?`, `instanceId`}) 🡒 (`void`| Promise) **Default:**– | Used for dynamically loading options. See [here](#delayed-loading) for detailed information. Possible values of `action`: `"LOAD_ROOT_OPTIONS"`, `"LOAD_CHILDREN_OPTIONS"` or `"ASYNC_SEARCH"`. `callback` - a function that accepts an optional `error` argument `parentNode` - only presents when loading children options `searchQuery` - only presents when searching async options `instanceId` - eqauls to the value of `instanceId` prop you passed to vue-treeselect |
| **matchKeys** | **Type:** String[] **Default:** `[ "label" ]` | Which keys of a `node` object to filter on. |
| **maxHeight** | **Type:** Number **Default:** `300` | Sets `maxHeight` style value of the menu. |
| **multiple** | **Type:** Boolean **Default:** `false` | Set `true` to allow selecting multiple options (a.k.a., multi-select mode). |
| **name** | **Type:** String **Default:**– | Generates a hidden `<input />` tag with this field name for html forms. |
| **noChildrenText** | **Type:** String **Default:** `"No sub-options."` | Text displayed when a branch node has no children. |
| **noOptionsText** | **Type:** String **Default:** `"No options available."` | Text displayed when there are no available options. |
| **noResultsText** | **Type:** String **Default:** `"No results found..."` | Text displayed when there are no matching search results. |
| **normalizer** | **Type:** Fn(`node`, `instanceId`) 🡒 `node` **Default:** `node => node` | Used for normalizing source data. See [here](#customize-key-names) for detailed information. |
| **openDirection** | **Type:** String **Default:** `"auto"` | By default (`"auto"`), the menu will open below the control. If there is not enough space, vue-treeselect will automatically flip the menu. You can use one of other four options to force the menu to be always opened to specified direction. Acceptable values: `"auto"`, `"below"`, `"bottom"`, `"above"` or `"top"`. |
| **openOnClick** | **Type:** Boolean **Default:** `true` | Whether to automatically open the menu when the control is clicked. |
| **openOnFocus** | **Type:** Boolean **Default:** `false` | Whether to automatically open the menu when the control is focused. |
| **options** | **Type:** `node[]` **Default:**– | Array of available options. See [here](#basic-features) to learn how to define them. |
| **placeholder** | **Type:** String **Default:** `"Select..."` | Field placeholder, displayed when there's no value. |
| **required** | **Type:** Boolean **Default:** `false` | Applies HTML5 `required` attribute when needed. |
| **retryText** | **Type:** String **Default:** `"Retry?"` | Text displayed asking user whether to retry loading children options. |
| **retryTitle** | **Type:** String **Default:** `"Click to retry"` | Title for the retry button. |
| **searchable** | **Type:**Boolean **Default:** `true` | Whether to enable searching feature or not. |
| **searchNested** | **Type:** Boolean **Default:** `false` | Set `true` if the search query should search in all ancestor nodes too. See [here](#nested-search) for example. |
| **searchPromptText** | **Type:** String **Default:** `"Type to search..."` | Text tip to prompt for async search. Used for [async search mode](#async-searching). |
| **showCount** | **Type:** Boolean **Default:** `false` | Whether to show a children count next to the label of each branch node. See [here](#disable-branch-nodes) for example. |
| **showCountOf** | **Type:** String **Default:** `"ALL_CHILDREN"` | Used in conjunction with `showCount` to specify which type of count number should be displayed. Acceptable values: `"ALL_CHILDREN"`, `"ALL_DESCENDANTS"`, `"LEAF_CHILDREN"` or `"LEAF_DESCENDANTS"`. |
| **showCountOnSearch** | **Type:** Boolean **Default:**– | Whether to show children count when searching. Fallbacks to the value of `showCount` when not specified. |
| **sortValueBy** | **Type:** String **Default:** `"ORDER_SELECTED"` | In which order the selected options should be displayed in trigger & sorted in `value` array. Use only when `:multiple="true"`. See [here](#flat-mode-and-sort-values) for example. Acceptable values: `"ORDER_SELECTED"`, `"LEVEL"` or `"INDEX"`. |
| **tabIndex** | **Type:** Number **Default:** `0` | Tab index of the control. |
| **value** | **Type:** `id`\|`node`\|`id[]`\|`node[]` **Default:**– | The value of the control. Should be `id` or `node` object when `:multiple="false"`, or an array of `id` or `node` object when `:multiple="true"`. Its format depends on the `valueFormat` prop. For most cases, just use `v-model` instead. |
| **valueConsistsOf** | **Type:** String **Default:**`"BRANCH_PRIORITY"` | Which kind of nodes should be included in the `value` array in multi-select mode. See [here](#prevent-value-combining) for example. Acceptable values: `"ALL"`, `"BRANCH_PRIORITY"`, `"LEAF_PRIORITY"`, `"SECOND_LEAF_PRIORITY"` or `"ALL_WITH_INDETERMINATE"`. |
| **valueFormat** | **Type:** String **Default:**`"id"` | Format of `value` prop. Note that, when set to `"object"`, only `id` & `label` properties are required in each `node` object in `value`. Acceptable values: `"id"` or `"object"`. |
| **zIndex** | **Type:** Number \| String **Default:** `999` | `z-index` of the menu.|
| **showTooTip** | **Type:** Boolean  **Default:** `false` | Whether to show Tooltip.  |


### Documentation & Live Demo

[Visit the website](https://vue-treeselect.js.org/)

Note: please use a desktop browser since the website hasn't been optimized for mobile devices.

### Browser Compatibility

- Chrome
- Edge
- Firefox
- IE ≥ 9
- Safari

It should function well on IE9, but the style can be slightly broken due to the lack of support of some relatively new CSS features, such as `transition` and `animation`. Nevertheless it should look 90% same as on modern browsers.

### Contributing

1. Fork & clone the repo
2. Install dependencies by `yarn` or `npm install`
3. Check out a new branch
4. `npm run dev` & hack
5. Make sure `npm test` passes
6. Push your changes & file a pull request
