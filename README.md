# Hugo Module - Feature Test

This Hugo module provides content, layouts, and configuration to test various Hugo features.

## Feature tests

When you add this module to a project, the build will perform the following tasks. Some require manual inspection of the output to fully verify.

- Import components from a Hugo module.
- Import a content file named `hugö.md` to verify that the Git `core.quotepath` setting is `false`.[^1]
- Extract the Git author date from the imported content.
- Verify that the embedded link and image render hooks are enabled and functioning properly.
- Perform vendor prefixing of CSS rules using the `postcss`, `postcss-cli`, and `autoprefixer` Node.js packages.
- Transpile modern JavaScript syntax to a safe, cross-browser equivalent using the `@babel/core`, `@babel/cli`, and `@babel/preset-env` Node.js packages.[^2]
- Transpile Sass to CSS using Dart Sass.
- Process CSS files using the `tailwindcss` and `@tailwindcss/cli` Node.js packages.
- Decode and resize an AVIF image, then encode to all supported image formats.
- Decode and resize a WebP image, then encode to all supported image formats.
- Render Markdown content.
- Render Emacs Org mode content.
- Render HTML content.
- Render AsciiDoc content.[^3]
- Render Pandoc content.[^4]
- Render reStructuredText content.[^5]

[^1]: See [issue #9810](https://github.com/gohugoio/hugo/issues/9810).
[^2]: For most modern projects, using Hugo's built-in `js.Build` function is preferred over Babel, as it handles bundling and transpilation natively without requiring external Node.js dependencies.
[^3]: You must install Asciidoctor and its dependencies (Ruby) to render the AsciiDoc content format.
[^4]: You must install Pandoc to render the Pandoc content format.
[^5]: You must install Docutils and its dependencies (Python) to render the reStructuredText content format.


## Configuration

### Initialize the module

To add this module to your project, initialize your project as a Hugo module:

```sh
hugo mod init foo
```

In the above, `foo` is typically something like `github.com/user/project`.

### Configure your site

Then add this to your site configuration:

```toml
enableGitInfo = true

[caches]
  _merge = 'deep'
  
[cascade]
  _merge = 'deep'

[markup]
  _merge = 'deep'

[security]
  _merge = 'deep'

[[module.imports]]
  path = 'github.com/jmooring/hugo-module-feature-test'
```

### Install Node dependencies

Now install the Node dependencies:

```sh
hugo mod npm pack
npm i
```

### Version control

Make sure to check these files into source control:

```text
packages/**
package.json
package-lock.json
```

## Usage

To test the rendering of AsciiDoc, Pandoc, or reStructuredText using the module's example files, ensure you have the respective external converters installed and build your project with the `--environment` flag:

```sh
hugo --environment with-external-converters
```

Or use the shorthand notation:

```sh
hugo -e with-external-converters
```

Or set the `HUGO_ENVIRONMENT` environment variable to `with-external-converters`.

## Installing external converters

To install the external converters on Debian and its derivatives:

```sh
sudo apt update
sudo apt install -y asciidoctor
sudo apt install -y pandoc
sudo apt install -y python3-docutils
```
