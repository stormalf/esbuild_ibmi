# esbuild for IBMi

This repo contain some changes to build esbuild for IBMi.

to compile it after cloning this repo :

    cd esbuild_ibmi
    make platform-os400-ppc64
    cd npm/@esbuild/os400-ppc64
    npm i
    npm i -g
    cd ../../esbuild
    cp -r ../@esbuild/os400-ppc64/bin .
    npm i -g

and if all is correct :

    esbuild --version
    shows 0.24.0

## current status concerning grafana on IBMi (grafana frontend)

Issue with package installed on IBMi that shows relative path to bin folder when executing npm list -g.
I tried verdaccio private npm package. 
A trick with verdaccio is to change the config.yaml to comment #proxy: npmjs and put proxy: false. After that yarn publish --registry http://localhost:4873 works. After revert config.yaml and set proxy:npmjs.
Now yarn install continues to fail with exit 1 and showing postinstall in comment (not sure why). As a workaround, go to grafana/node_modules/esbuild and npm i works fine.
Other issue is with esbuild-loader/node_modules/esbuild. The workaround is to copy the ./node_modules/esbuild folder to replace the esbuild-loader/node_modules/esbuild.
Changed the package.json from grafana to set 0.24.0 and not 0.21.5 for esbuild and qualifying esbuild with absolute path on IBMi.
For Grafana on IBMi, I will create a new github repo when Grafana frontend is ready to work.

Last issue :
yarn run build failed at 92% when processing SourceMapDevToolPlugin with javascript heap out of memory.

In resume : 
yarn install => continues to fail
yarn run themes-generate => works fine
yarn run build => 92% failed with javascript heap out of memory





<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./images/wordmark-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="./images/wordmark-light.svg">
    <img alt="esbuild: An extremely fast JavaScript bundler" src="./images/wordmark-light.svg">
  </picture>
  <br>
  <a href="https://esbuild.github.io/">Website</a> |
  <a href="https://esbuild.github.io/getting-started/">Getting started</a> |
  <a href="https://esbuild.github.io/api/">Documentation</a> |
  <a href="https://esbuild.github.io/plugins/">Plugins</a> |
  <a href="https://esbuild.github.io/faq/">FAQ</a>
</p>

## Why?

Our current build tools for the web are 10-100x slower than they could be:

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./images/benchmark-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="./images/benchmark-light.svg">
    <img alt="Bar chart with benchmark results" src="./images/benchmark-light.svg">
  </picture>
</p>

The main goal of the esbuild bundler project is to bring about a new era of build tool performance, and create an easy-to-use modern bundler along the way.

Major features:

- Extreme speed without needing a cache
- [JavaScript](https://esbuild.github.io/content-types/#javascript), [CSS](https://esbuild.github.io/content-types/#css), [TypeScript](https://esbuild.github.io/content-types/#typescript), and [JSX](https://esbuild.github.io/content-types/#jsx) built-in
- A straightforward [API](https://esbuild.github.io/api/) for CLI, JS, and Go
- Bundles ESM and CommonJS modules
- Bundles CSS including [CSS modules](https://github.com/css-modules/css-modules)
- Tree shaking, [minification](https://esbuild.github.io/api/#minify), and [source maps](https://esbuild.github.io/api/#sourcemap)
- [Local server](https://esbuild.github.io/api/#serve), [watch mode](https://esbuild.github.io/api/#watch), and [plugins](https://esbuild.github.io/plugins/)

Check out the [getting started](https://esbuild.github.io/getting-started/) instructions if you want to give esbuild a try.
