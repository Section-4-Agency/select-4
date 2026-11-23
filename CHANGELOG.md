# Changelog

## 1.0.0

First release of Select 4, forked from Nice Select 2 v2.1.0.

### Added

- `select2-more-search` option attribute: extra words matched by the search.
- `select2-text-prepend` and `select2-text-append` option attributes: text rendered around the option label.
- Custom search function through the `select2-search-fn` attribute or the `searchFnName` option.
- Multi-word search: every word of the query must match.
- `window.Select4` global. `window.NiceSelect` is kept as an alias.

### Fixed

- Multiple mode crashed when rendering the selected items (`this` was undefined inside the callback).
- Options built from `data` no longer match the word "undefined" in search.
