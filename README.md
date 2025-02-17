<img alt="" align="right" width="200" src="src/assets/sdl.png">

# The STALKER Developers Library

This repo contains the source content and build scripts for the STALKER Developers Library (SDL). It aims to document the immense tribal knowledge of the STALKER modding community and covers game engine details, the X-Ray Software Editing Kit, community tools, and guides for map-making.

## Contributing
The library is not directly editable by its readers. This allows the editing team to verify information before it's added. However, we want and need the community's help filling in gaps. If you want to submit information or join the editing team, see the [Contributing page]().

## Development
The codebase is essentially a [static site](https://en.wikipedia.org/wiki/Static_web_page) generator. We use [Gulp](https://gulpjs.com/) as the build task runner, with various tasks to process stylesheets, render pages, bundle JS ([esbuild](https://esbuild.github.io/)), and copy assets. All build results go into a `dist` folder that is ready to serve.

Content is written in a combination of [Markdoc-flavoured markdown](https://markdoc.dev) and YAML files for structured data, which are rendered to HTML using [Preact](https://preactjs.com/) in TypeScript. Pages are also rendered in plaintext form and bundled into a client-side search index using [Minisearch](https://lucaong.github.io/minisearch/). We use [Sass](https://sass-lang.com/) as a CSS preprocessor.

### Building and testing
In order to see content as it will appear online, you can run SDL in development mode. As a pre-requisite this project requires installing at least [Node.js v14+](https://nodejs.org/en/) and [Git LFS](https://git-lfs.github.com/).

If you have installed Git LFS _after_ checking out the project already, you'll need to run `git lfs install` and `git lfs pull` to download the objects. If you forget to do this the build will fail because `ffmpeg` will be unable to read video files as videos ("Invalid data found when processing input").

Once those are installed, clone the project and run these shell commands to get the site running locally:

```sh
# install dependencies (run once)
npm ci

# start the development server
npm run dev
```

You can now visit http://localhost:8080/ in a browser and see the website. Edit content source files, then refresh your browser to see changes. You can run the server on a different port with `SDL_PORT=9001 npm run dev`.

The development server renders pages on-demand, but you can also run `npm run static` to fully render all pages to HTML and serve them. A full static build takes longer and isn't recommended for quick content writing. You can use it as a final step to verify the build will work once changes are merged. Note: [FFmpeg](https://ffmpeg.org/) is an optional dependency used to generate video thumbnails during a full build. It needs to be available on your system `PATH`. Windows users can simply download `ffmpeg.exe` and place it in the project root. If you don't want to set up FFmpeg just run `SDL_NO_THUMBNAILS=true npm run static` and thumbnails won't be used.

### Technical goals
An explicit choice was made to avoid typical managed or self-hosted Wiki platforms for this library and instead build a static site generator with custom features for STALKER. The main tenets are:

* No API or dynamic content: the site should be easy to host and test locally with any HTTP server capable of serving files, and is easily cached on a CDN. No compute needed means low hosting costs. Even the search index is client-side.
* Respect the time of the editors. Wiki features should empower them to write faster and easier. Nobody will write if it's a chore.
* Semantic HTML: Page structures are document-like and use the right elements for the job to maintain accessibility.
* Mobile-friendly: Pages should be responsive and readable on mobile.
* The website should make minimum use of client side JavaScript unless there are interactive features needed.

Non-goals are user accounts, live editing, and on-site discussion pages. We use the pull request model and Discord discussions to ensure new information is vetted.

## License
SDL's codebase is licensed under version 3.0 of the GNU General Public License. A copy of its text can be found in COPYING.

The content of its pages, including articles, guides, images, tag descriptions, and other rendered metadata are available under the under the [CC BY-SA 3.0 license][cc-license].

[s3-origin]: http://reclaimers-c20.s3-website-us-east-1.amazonaws.com/
[cc-license]: https://creativecommons.org/licenses/by-sa/3.0/
