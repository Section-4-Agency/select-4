# Select 4

A lightweight Vanilla JavaScript plugin that replaces native `<select>` elements with customizable dropdowns.

Select 4 is a fork of [Nice Select 2](https://github.com/bluzky/nice-select2) **v2.1.0** by Dung Nguyen, maintained by Section 4. It keeps the original API and markup and adds richer option rendering and search.

## What's different from Nice Select 2

- **Extra search terms per option**: `select2-more-search`
- **Text before or after an option label**: `select2-text-prepend` and `select2-text-append`
- **Multi-word search**: each space-separated word must match the option text or its extra search terms, in any order. Each word is read as a regular expression, as in Nice Select 2.
- **Custom search function**: `select2-search-fn` attribute or `searchFnName` option
- **Global name**: `window.Select4`. `window.NiceSelect` stays available as an alias.

The generated markup and CSS classes (`.nice-select`, `.nice-select-dropdown`, `.option`…) are unchanged, so existing styles keep working.

## Install

From GitHub, pinned to a tag:

```bash
npm install github:Section-4-Agency/select-4#v1.0.0
```

The package ships pre-built files only:

```
dist/js/select-4.js    UMD build (script tag, CommonJS, AMD)
dist/css/select-4.css
```

## Usage

```html
<link rel="stylesheet" href="path/to/select-4.css" />
<script src="path/to/select-4.js"></script>
```

```js
Select4.bind(document.getElementById("a-select"), {
  searchable: true,
  placeholder: "Select an option",
  searchtext: "Search",
  selectedtext: "selected",
});
```

With a bundler:

```js
import Select4, { bind } from "select-4";
import "select-4/dist/css/select-4.css";

new Select4(document.getElementById("a-select"), { searchable: true });
// or
bind(document.getElementById("a-select"), { searchable: true });
```

### Options

| Option | Default | Description |
| --- | --- | --- |
| `searchable` | `false` | Show a search box in the dropdown |
| `placeholder` | `"Select an option"` | Text shown when nothing is selected. Can also be set with the `placeholder` attribute. |
| `searchtext` | `"Search"` | Search box placeholder. Can also be set with the `searchtext` attribute. |
| `selectedtext` | `"selected"` | Suffix for the selection count in multiple mode. Can also be set with the `selectedtext` attribute. |
| `showSelectedItems` | `false` | In multiple mode, always list the selected items instead of showing a count |
| `data` | `null` | Build the options from an array instead of the `<option>` elements |
| `searchFnName` | — | Name of a global function used to filter options (see below) |

### Option attributes

```html
<select id="country">
  <option value="fr"
          select2-text-prepend="🇫🇷"
          select2-text-append="+33"
          select2-more-search="france french">France</option>
</select>
```

| Attribute | Effect |
| --- | --- |
| `select2-text-prepend` | Rendered before the label in `<span class="s4_text_prepend">` |
| `select2-text-append` | Rendered after the label in `<span class="s4_text_append"> - …</span>` |
| `select2-more-search` | Extra words the search matches, not displayed |

The prepend and append values are inserted as HTML. Never put user-supplied content in them.

### Custom search function

Set `select2-search-fn` on the `<select>`, or pass `searchFnName`, with the name of a function available on `window`:

```html
<select select2-search-fn="mySearch">…</select>
```

```js
window.mySearch = function (query, option, selectElement) {
  // query: trimmed, lower-cased search text
  // option.data: { text, value, s4_search, s4_text_prepend, s4_text_append, … }
  return option.data.text.toLowerCase().includes(query);
};
```

Return `true` to show the option and `false` to hide it. The function is called for every option, including when the query is empty.

### Instance methods

- `update()`: update the dropdown items to match the source `<select>`
- `disable()`: disable the select
- `enable()`: enable the select
- `destroy()`: remove the generated dropdown
- `clear()`: clear all selected options

### Events

Besides `change`, the native `<select>` receives `modalopen` and `modalclose` when the dropdown opens and closes.

## License

[MIT](LICENSE). Original work Copyright (c) 2021 Dung Nguyen. Modifications Copyright (c) 2025 Section 4.
