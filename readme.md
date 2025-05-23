<h1><img src="https://digital.gov/img/digitalgov-logo.svg" alt="Digital.gov Logo"/></h1>

## We help people in government build better digital services

https://digital.gov

- Sign-up for the [Digital.gov newsletter »](https://digital.gov/about/subscribe/)
- Follow us on [LinkedIn »](https://www.linkedin.com/company/digitalgov-gsa)
- Follow us on [X (formerly Twitter) »](https://twitter.com/Digital_Gov/)
- Like our page on [Facebook »](https://www.facebook.com/DigitalGov/)
- Watch our videos and subscribe to our channel on [YouTube](https://www.youtube.com/@DigitalGov)

Want to learn more about how we work? [Check out our Wiki page »](https://github.com/GSA/digitalgov.gov/wiki)

---

## Repositories

As a product, [Digital.gov](https://digital.gov) maintains a collection of repositories. All of our work is open source and we encourage you to take a look at and contribute to our projects by submitting a Pull Request, a GitHub Issue, or commenting on existing Issues and Pull Requests.

The repositories below are all used to maintain [Digital.gov:](https://digital.gov).

<details>
  <summary>Platform</summary>

| Project                                                         | Description                                                                                                                                              |
| --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [GSA/**digitalgov.gov**](https://github.com/GSA/digitalgov.gov) | (This repo) Site platform currently deployed as a static site built with [Hugo](https://gohugo.io/) and hosted by [cloud.pages.gov](https://cloud.gov/). |
| [18F/**dns**](https://github.com/18F/dns)                       | DNS configuration for digital.gov domains managed by GSA TTS.                                                                                            |
| [uswds/**uswds**](https://github.com/uswds/uswds)               | This site is developed using the U.S. Web Design System v2, managed by GSA TTS.                                                                          |

</details>

<details>
  <summary>Tools - projects we have created in order to better aid our work on the digital.gov platform.</summary>

| Project                                                                                    | Description                                                                      |
| ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| [GSA/**digital.gov-design**](https://github.com/GSA/digital.gov-design)                    | A collection of design assets used for the digital.gov platform.                 |
| ~[GSA/**digitalgov-workflow**](https://github.com/GSA/digitalgov-workflow)~ (**archived**) | A tool for managing the digital.gov editorial workflow on GitHub.                |
| ~[GSA/**redir**](https://github.com/GSA/redir)~ (**archived**)                             | A basic [Jekyll](https://jekyllrb.com/) template to use for temporary redirects. |

</details>

---

## Development Guide

### Technologies you should be familiarize yourself with

- [Hugo](https://gohugo.io/documentation/) - The primary site engine that builds digital.gov code and content.
- [Front Matter](https://gohugo.io/content-management/front-matter#readout) - The top of each page/post includes keywords within `---` tags. This is meta data that helps Hugo build the site, but you can also use it to pass custom variables.
- [U.S. Web Design System v3.0](https://designsystem.digital.gov) - the design system used in digital.gov.
- [Gulp](https://gulpjs.com/) - the asset pipeline.

### Installation

#### Prerequisites

Unix-based systems are recommended for development. If you are using Windows, consider using the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install) to run a Unix-based system on your machine.
If you do not have a Unix-based system, you will receive additional linting errors when running the `npm run lint` commands.

Install [Gulp](https://gulpjs.com/) globally from your terminal command line:

```bash
npm install gulp-cli -g
```

To use Gulp, you must have [Node](https://nodejs.org/) and [NPM](https://www.npmjs.com) installed.
We're currently using Node v18. A recommended way of changing your Node version is to use a node version manager tool like [`n`](https://www.npmjs.com/package/n) to quickly change between node versions.

NPM is package along with Node. Check your versions of these in your terminal command line by typing:

```bash
node -v
npm -v
```

Using [Homebrew](https://docs.brew.sh/) is a quick and easy way to install Hugo. [Install Homebrew](https://docs.brew.sh/Installation) before getting started.

#### Install Hugo 0.133.1

[Read the HUGO quickstart guide »](https://gohugo.io/getting-started/quick-start/)

**[For OSX](https://gohugo.io/getting-started/installing/#install-hugo-with-brew):**
`brew install hugo`
_see https://gohugo.io/getting-started/installing/ for other OSs_

Quickly check your Hugo version at your terminal command line by running:

```bash
hugo version
```

**Note:** Digital.gov currently uses Hugo version 0.133.1. This is noted in our [.hugo-version](.hugo-version) file.
If Hugo has released a new version, but digital.gov hasn't been upgraded to that version, you may get errors when building locally. It is possible to use Homebrew to download a previous version of Hugo. To do that follow these instructions:

1.  Uninstall the current version with `brew uninstall hugo`
2.  Visit
    [<u>https://github.com/Homebrew/homebrew-core/blob/master/Formula/h/hugo.rb</u>](https://github.com/Homebrew/homebrew-core/blob/master/Formula/h/hugo.rb)
3.  Click the “History” link
4.  Find the “bottle” commit for the desired version (Ex: 'hugo: update 0.133.1' bottle)
5.  Press the “View at this point in history” button
6.  Press the “Raw” button
7.  Right-click anywhere on the page and choose “Save as…”
8.  Save hugo.rb to any directory (home, downloads, etc.)
9.  Open a terminal
10. CD into the directory where you saved the hugo.rb file
11. Install with `brew install hugo.rb`
12. Prevent automatic updates with `brew pin hugo`

#### Setup

Once the prerequisites are installed, [clone the repository](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository) to your local machine. Then navigate to the project folder in your terminal and run:

```bash
npm install
```

This will install all of the Node dependencies needed to run your Hugo environment. This may take a little while!

#### Local Development

Running the local development server is as simple as running:

```bash
npm start
```

NPM will run the following scripts:

- `gulp env` — sets the environment variable to development (local builds only, not in Federalist)
- `gulp` — builds and compresses all of the SCSS and JS files, and copies jquery and uswds js from `node_modules` and puts them in the `/dist/` folder.
- `gulp watch` — starts a watch task to look for changes in the SCSS and JS files
- `hugo serve` — builds all of the pages in hugo and creates a local server at `http://localhost:1313/`

When Hugo is done building, you should see a success message like:

```bash
Web Server is available at //localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

You may then view your local site in the browser at `http://localhost:1313/`.

Local development is powered by Gulp tasks to allow rapid development through:

- A local development server at `http://localhost:1313/`.
- Automatic CSS & JS updates without reloading the page
- Automatic page reloads when content is changed

### Configuration

#### Environment Variables

This project uses environment variables to handle uploading of images to AWS (powered by Gulp scripts).

In your command line terminal run `cp env.example .env` to create a template .env file in the root directory of the project.

Replace “[your key goes here]” in the .env file with your AWS key.

#### Asset Pipeline

_NOTE: This is now included in the `npm start` command above_

All style and image build tasks are handled by [Gulp](https://gulpjs.com/docs/en/getting-started/javascript-and-gulpfiles) and are located in `gulpfile.js`. All parts of the build are configurable in discrete files (located in config/gulp) to make management easy.

Starting the gulp watch tasks to compile styles. This can be done in the terminal command line by running:

```bash
gulp
```

You would want to have the Hugo build running along with a `gulp` session in separate terminal sessions in order to compile and watch both content and style changes.

**Tip:** Use the keyboard shortcut `control + c` to stop the gulp watch process.

### Images

Digital.gov uses a hybrid image processing system that combines Hugo's built-in image processing with AWS S3 storage:

#### Image Processing System

Images found in `content/images/inbox/` are handled in two ways simultaneously:

1. Optimized and compressed then sent to an AWS S3 bucket via `gulp img`
2. Processed by Hugo's built-in image processing to create responsive variants (800px and 1200px)

This dual approach ensures:

- Optimized image delivery through S3
- Responsive image variants through Hugo
- Fallback paths when either system isn't available
- Support for external images through direct URLs

#### Setting up AWS Credentials

1. Copy the environment template:
   ```bash
   cp env.example .env
   ```

2. Add your AWS credentials to the `.env` file:
   ```
   AWS_ACCESS_KEY_ID=[your access key]
   AWS_SECRET_ACCESS_KEY=[your secret key]
   ```

3. Mount the S3 bucket:
   ```bash
   npm run mount-s3
   ```

#### Using the Image Shortcode

The `img` shortcode provides flexible image handling with both S3 and Hugo processing:

```go
{{< img src="path/to/image.jpg" alt="Description" align="center" caption="My caption" credit="Photo by John Doe" >}}
```

Parameters:

- `src`: path to the image (required)
- `alt`: alt text for accessibility (required)
- `align`: alignment (left/center/right, optional)
- `caption`: image caption (optional)
- `credit`: image credit (optional)

**Other helpful HUGO commands:**

- `hugo` — builds all the pages in the site, without creating a server
- `hugo serve` — builds all of the pages in hugo and creates a local server at `http://localhost:1313/`
- `hugo serve --templateMetricsHints` — for seeing where you can apply caching in templates and speed up the build time
  [See more in the Hugo docs »](https://gohugo.io/commands/hugo/)

## Upgrading Hugo

1. Read through [the recent releases](https://github.com/gohugoio/hugo/releases)
2. Run `brew upgrade hugo` to upgrade your local copy ([docs](https://gohugo.io/getting-started/installing/#upgrade-hugo)).
3. Set the version in the `.hugo-version` file. This is only used for telling Federalist which version of Hugo they should checkout and use.
4. Update this README.md to show the current hugo version
5. Update the version in `.circleci/config.yml to ensure that the same version of Hugo is being used for CI.

## Accessibility tests

We follow the WCAG2AA standard, and one of the ways we check that we're following the right rules is through automated tools, like [**pa11y**](https://github.com/pa11y/pa11y/). For more info on the rules being tested checkout the [pa11y wiki](https://github.com/pa11y/pa11y/wiki/HTML-CodeSniffer-Rules).

### Running tests

> **Warning**
> Site must be running locally to perform the scan.

To run a web accessibility test on digital.gov do the following:

1. Check out the site from GitHub https://github.com/GSA/digitalgov.gov/
1. Install and run the site locally following the `Install` and `Run` instructions above.
1. In a separate terminal window, run `npm run test:pa11y` to initiate the accessibility checker.

Accessibility testing configuration is located in the .pa11yci file.

## Linters

To test the validity of API JSON files, run `npm run lint:json` in the terminal on your local machine. This will check the validity of the Hugo generated JSON files used for the API. Currently, it validates authors, images, and topics using the tool `jsonlint`. If an issue is found with the JSON, `jsonlint` will return a non-zero exit code causing CircleCI to fail. See the [wiki API page](https://github.com/GSA/digitalgov.gov/wiki/APIs) for fixing API issues.

Markdown testing can be performed by running `npm run lint:markdown`. The rules that are used for the linter can be found in `.markdown-lint.yml`.

HTML linting can be performed by running 'npm run test:htmlproofer'.
To have HTMLproofer ignore certain content see: https://github.com/gjtorikian/html-proofer#ignoring-content

## Common Regex scripts

### convert legacy-img to standard img

```bash
{{< legacy-img src="/\d+/\d+/\d{2,4}[-x]+\d{2,4}[_-]*(.+?)\.[pngje]+"(
alt=".+?")* >}}
```

```bash
{{< img src="$1"$2 >}}
```

### convert CDN links

```bash
{{< legacy-img src="/(\d{4,4}) {{< legacy-img src="$1
```

### replace `url` with `slug` in posts

```bash
^url: .+/([^/]+)\.md
slug: $1
```

### New Features
- Communities of Practice Job Board
  - [Development Guide](./themes/digital.gov/layouts/job-board/readme.md)
  - [Demo](https://federalist-466b7d92-5da1-4208-974f-d61fd4348571.sites.pages.cloud.gov/preview/gsa/digitalgov.gov/kl-job-board-mvp/job-board/)
