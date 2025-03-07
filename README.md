# Pale Moon Web Technologies Polyfill Add-On

Inject Polyfills for various web technologies into pages requiring them. This addon is aimed
at UXP and Pale Moon. Seamonkey support is mostly untested.

Polyfills are specified as "fixes" that are applied per domain. Fixes currently can be:

  * scripts that must be loaded
  * injected inline-scripts
  * Content-Security-Policy adjustments
  * script content changes

It is possible to specify any combination of required fixes for a site.

## Rule Syntax

Rules are made up of two parts: at least one selector and at least one fix.

**Fixes** can be any number of actions, best refer to [function evaluateFix](lib/main.js) for
up-to-date info on what each one does. The names are case-sensitive.

**Selectors** use a syntax derieved from Adblock filters. Three parts are used:

  * the domain part (*mandatory*)
  * path part (*optional*)
  * delimted with a "$": content type selection (*optional*)
      * document: regular top-level document
      * subdocument: included document, such as frame or iframe
      * script: anything included via <script> tags

All of these are valid selectors:
```
example.com
example.com/path/a.html
example.com/path/to.js$script
example.com/path/any*.js$script
example.com$subdocument
```

**Rule scripts** are constructed by giving any number of selectors followed by a comma-separated list
of the fixes to apply, indented by whitespace:
```
example.com
example.com/path/a.html
  std-queueMicrotask,std-customElements
```

Additionally, the exclusion script has a special case: if the special fix `*` is used, all fixes are
suppressed for the matched sites. This is useful when running this addon alongside others that also
apply changes. For example, the following rule disables all fixes on `github.com`:
```
github.com
  *
```


## Credits

This addon is heavily based on [**GitHub Web Components Polyfill**](https://github.com/JustOff/github-wc-polyfill),
which does the same thing for GitHub and a few other sites.
```
 Portions based on GitHub Web Components Polyfill Add-on
 Copyright (c) 2020 JustOff. All rights reserved.
 Copyright (c) 2022 SeaHOH. All rights reserved.
 https://github.com/JustOff/github-wc-polyfill
```

The polyfills themselves have different contributors, see `lib/polyfills.js`.

The following people have contributed to this addon:

  * [roytam1](https://github.com/roytam1)
  * [UCyborg](https://github.com/UCyborg)

