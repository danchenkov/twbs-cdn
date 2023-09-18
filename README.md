# README

I am trying to choose the best of at least approproate Asset Pipeline for my apps.

The project is using Bootstrap 5, not so much for styles and perks, but mainly because it illustrates the use of external library with JS and CSS components. JS part has dependency on popper.js and CSS part has optional config for Sass.

| Technology      | Description                   |
| --------------- | ----------------------------- |
| Asset Pipeline  | propshaft                     |
| Bootstrap       | CDN                           |
| Sass processing | -                             |
| CSS minificaton | -                             |
| JS minification | -                             |
| Naming          | importmaps                    |
| Bundling        | Deemed unnecessary for HTTP/2 |

### Basic needs for a quick start

- bundled and minified Bootstrap 5: use CDN
- local styles already bundled / minified: this is the weak point, need Sass bundler or at least CSS minifier, adding sassc-rails brings about sprockets as dependency for Asset Pipeline.
- assets fingerprinting for production: Propshaft

### Keynote

From [Migrating from Sprockets](https://github.com/rails/propshaft)
Propshaft does a lot less than Sprockets, by design, so it might well be a fair bit of work to migrate if it's even desirable. This is particularly true if you rely on Sprockets to provide any form of transpiling, like CoffeeScript or Sass, or if you rely on any gems that do. You'll need to either stop transpiling or use a Node-based transpiler, like those in jsbundling-rails and cssbundling-rails.

On the other hand, if you're already bundling JavaScript and CSS through a Node-based setup, then Propshaft is going to slot in easily. Since you don't need another tool to bundle or transpile. Just to digest and serve.

But for greenfield apps using the default import-map approach, Propshaft can also work well, if you're able to deal with vanilla CSS.

#### JS handling

Importmaps is included. It allows simpler reference providing a nickname to imported JS assets (whether CDN or gem or vendor folder or local folder). JS libraries have to be modularized. References can be quickly swapped (say, from gem to CDN) without changing a nickname.
JS source folder with umninified, unbundled assets is currently under `app/javascript`, not `app/assets/javascript`.

#### CSS handling

If you have to have Sass, you need to use dartsass-rails or sassc-rails. Otherwise, CSS is handled by the Asset Pipeline.

#### Asset Pipeline

Propshaft does not minify assets, it only handles assets paths and digital stamping / fingerprinting. Since if handles paths, it decodes `url(asset)` to `url(digested-asset)` in CSS files. Apparently CSS files do not have to be ERB for that to work.
