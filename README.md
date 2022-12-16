# Hosting Test - Netlify

This is a test of hosting a Hugo site on Netlify.

The site requires:

- The dart-sass-embedded executable to transpile Sass to CSS
- Installation of Node.JS dependencies
- Go to pull in a content Module

## Embedded Dart Sass

Different techniques for installing the Dart Sass transpiler...

### Node.js

Using the Node.js package, this site took 14s to deploy.

netlify.toml

```text
[build]
command = """\
  npm install "sass-embedded@${DART_SASS_VERSION}" && \
  path_nm=/opt/build/repo/node_modules && \
  path_dse=sass-embedded-linux-x64/dart-sass-embedded/dart-sass-embedded && \
  cp "${path_nm}/${path_dse}" "${path_nm}/.bin" && \
  hugo --gc --minify
  """
publish = "public"

[build.environment]
DART_SASS_VERSION = "1.56.2"
HUGO_VERSION = "0.108.0"
TZ = "America/Los_Angeles"
```

### Brew

Using Brew, this site took 1m 47s to deploy.

netlify.toml

```text
[build]
command = "hugo --gc --minify"
publish = "public"

[build.environment]
HUGO_VERSION = "0.108.0"
HOMEBREW_BUNDLE_FILE = "netlify.brewfile"
TZ = "America/Los_Angeles"
```

netlify.brewfile

```text
# Install Embedded Dart Sass
tap "sass/sass"
brew "dart-sass-embedded"
```
