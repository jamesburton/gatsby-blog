# Gatsby Serverless Blog

## References
* Gatsby Quickstart - https://www.gatsbyjs.org/docs/quick-start/
* Contentful - https://www.gatsbyjs.com/guides/contentful/
	* https://www.gatsbyjs.org/packages/gatsby-source-contentful/
* StoryBlok - https://www.storyblok.com/tp/gatsby-multilanguage-website-tutorial
	* https://github.com/storyblok/gatsby-source-storyblok

## Steps

* `npm i -g gatsby-cli@latest
* `gatsby new gatsby-blog`
* `cd gatsby-blog`
* `yarn run develop` (or `gatsby develop`)
* Test that default content (from `src/pages`) is served correctly (http://localhost:8000)
* Test the graphql interface (http://localhost:8000/___graphql)
* Stop the server (Ctrl-C)
* If adding Contentful:
	* `yarn add gatsby-source-contentful`
	* Modify gatsby-config.js to include:
```
// Inside module.exports = { plugins: [ /* Add here */ ] } }
    {
      resolve: `gatsby-source-contentful`,
      options: {
        spaceId: `your_space_id`,
        // Learn about environment variables: https://gatsby.dev/env-vars
        accessToken: process.env.CONTENTFUL_ACCESS_TOKEN,
	// If using preview API, specify the preview host value (comment out otherwise):
	host: `preview.contentful.com`,
	// If local download/cache of contenful is required (such as local (reduce contentful usage) and offline/disconnect-from-contentful build is required)
	downloadLocal: true,
      },
    },
```
	* Update .env.development (or whichever .env) to include settings
		See https://www.gatsbyjs.org/docs/environment-variables/
	* Modify gatsby-config.js to use dotenv (to support windows)
```
require("dotenv").config({
  path: `.env.${process.env.NODE_ENV}`,
})
// Now the variables are available on process.env as usual.
```
	* On linux, environment variables can be used like this: ```MY_ENV_VAR=foo npm run develop```
	* Example `.env.development`:
```
GATSBY_API_URL=https://dev.example.com/api
API_KEY=927349872349798
```
	* Example of using environemnt variables at runtime (as Gatsby uses the webpack DefinePlugin)
``` JSX
// In any frontend code
render() {
  return (
    <div>
      <img src={`${process.env.GATSBY_API_URL}/logo.png`} alt="Logo" />
    </div>
  )
}```
	* All `GATSBY_` prefixed environment variables are available server-side without prefix e.g. for `GATSBY_API_KEY`:
``` JS (Server-side)
// In any server-side code, e.g. gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-patronus`,
      options: {
        apiKey: process.env.API_KEY,
      },
    },
  ],
}
```
* If adding StoryBlok:
	* `yarn add gatsby-source-storyblok storyblok-react`
	* Modify gatsby-config.js to include:
```
// Inside module.exports = { plugins: [ /* Add here */ ] } }
    {
      resolve: 'gatsby-source-storyblok',
      options: {
        accessToken: 'YOUR_TOKEN', // Use a 'preview' token is selecting 'draft' for 'version' below
        homeSlug: 'home', // Used for the root level /
        version: 'draft', // 'draft' or 'published'
      }
    }
```
	* Continue from "Creating the editor page": https://www.storyblok.com/tp/gatsby-multilanguage-website-tutorial#creating-the-editor-page
-----
* If adding Cloudinary:
	* See https://cloudinary.com/blog/introducing_cloudinary_s_gatsby_plugins
		* 
* Other Source Options
	* Filesystem: https://www.gatsbyjs.org/packages/gatsby-source-filesystem/
	* CSV: https://www.gatsbyjs.org/packages/gatsby-transformer-csv/
	* Vimeo
		* Working with video: https://www.gatsbyjs.org/docs/working-with-video/
		* Using Node SDK to render in `<video />` tag: https://www.gatsbyjs.org/packages/gatsby-source-vimeo-all/
		* Using remark video embed: https://scotch.io/tutorials/embedding-videos-in-your-gatsbyjs-sites
	* JSON: https://www.gatsbyjs.org/packages/gatsby-transformer-json/
	* Netlify CMS: https://www.gatsbyjs.org/packages/gatsby-plugin-netlify-cms/
		* NB: Full Gatsby Netlify instructions: https://www.netlify.com/blog/2016/02/24/a-step-by-step-guide-gatsby-on-netlify/
	
* Hosting and Analytics	
	* Netlify: https://www.gatsbyjs.org/packages/gatsby-plugin-netlify/
	
* Other Plugins/Modules to consider
	* https://www.gatsbyjs.org/packages/gatsby-plugin-react-helmet/
	* Robots: https://www.gatsbyjs.org/packages/gatsby-plugin-robots-txt/
	* Humans: https://www.gatsbyjs.org/packages/gatsby-plugin-humans-txt/

<!-- AUTO-GENERATED-CONTENT:START (STARTER) -->
<p align="center">
  <a href="https://www.gatsbyjs.org">
    <img alt="Gatsby" src="https://www.gatsbyjs.org/monogram.svg" width="60" />
  </a>
</p>
<h1 align="center">
  Gatsby's default starter
</h1>

Kick off your project with this default boilerplate. This starter ships with the main Gatsby configuration files you might need to get up and running blazing fast with the blazing fast app generator for React.

_Have another more specific idea? You may want to check out our vibrant collection of [official and community-created starters](https://www.gatsbyjs.org/docs/gatsby-starters/)._

## 🚀 Quick start

1.  **Create a Gatsby site.**

    Use the Gatsby CLI to create a new site, specifying the default starter.

    ```shell
    # create a new Gatsby site using the default starter
    gatsby new my-default-starter https://github.com/gatsbyjs/gatsby-starter-default
    ```

1.  **Start developing.**

    Navigate into your new site’s directory and start it up.

    ```shell
    cd my-default-starter/
    gatsby develop
    ```

1.  **Open the source code and start editing!**

    Your site is now running at `http://localhost:8000`!

    _Note: You'll also see a second link: _`http://localhost:8000/___graphql`_. This is a tool you can use to experiment with querying your data. Learn more about using this tool in the [Gatsby tutorial](https://www.gatsbyjs.org/tutorial/part-five/#introducing-graphiql)._

    Open the `my-default-starter` directory in your code editor of choice and edit `src/pages/index.js`. Save your changes and the browser will update in real time!

## 🧐 What's inside?

A quick look at the top-level files and directories you'll see in a Gatsby project.

    .
    ├── node_modules
    ├── src
    ├── .gitignore
    ├── .prettierrc
    ├── gatsby-browser.js
    ├── gatsby-config.js
    ├── gatsby-node.js
    ├── gatsby-ssr.js
    ├── LICENSE
    ├── package-lock.json
    ├── package.json
    └── README.md

1.  **`/node_modules`**: This directory contains all of the modules of code that your project depends on (npm packages) are automatically installed.

2.  **`/src`**: This directory will contain all of the code related to what you will see on the front-end of your site (what you see in the browser) such as your site header or a page template. `src` is a convention for “source code”.

3.  **`.gitignore`**: This file tells git which files it should not track / not maintain a version history for.

4.  **`.prettierrc`**: This is a configuration file for [Prettier](https://prettier.io/). Prettier is a tool to help keep the formatting of your code consistent.

5.  **`gatsby-browser.js`**: This file is where Gatsby expects to find any usage of the [Gatsby browser APIs](https://www.gatsbyjs.org/docs/browser-apis/) (if any). These allow customization/extension of default Gatsby settings affecting the browser.

6.  **`gatsby-config.js`**: This is the main configuration file for a Gatsby site. This is where you can specify information about your site (metadata) like the site title and description, which Gatsby plugins you’d like to include, etc. (Check out the [config docs](https://www.gatsbyjs.org/docs/gatsby-config/) for more detail).

7.  **`gatsby-node.js`**: This file is where Gatsby expects to find any usage of the [Gatsby Node APIs](https://www.gatsbyjs.org/docs/node-apis/) (if any). These allow customization/extension of default Gatsby settings affecting pieces of the site build process.

8.  **`gatsby-ssr.js`**: This file is where Gatsby expects to find any usage of the [Gatsby server-side rendering APIs](https://www.gatsbyjs.org/docs/ssr-apis/) (if any). These allow customization of default Gatsby settings affecting server-side rendering.

9.  **`LICENSE`**: Gatsby is licensed under the MIT license.

10. **`package-lock.json`** (See `package.json` below, first). This is an automatically generated file based on the exact versions of your npm dependencies that were installed for your project. **(You won’t change this file directly).**

11. **`package.json`**: A manifest file for Node.js projects, which includes things like metadata (the project’s name, author, etc). This manifest is how npm knows which packages to install for your project.

12. **`README.md`**: A text file containing useful reference information about your project.

## 🎓 Learning Gatsby

Looking for more guidance? Full documentation for Gatsby lives [on the website](https://www.gatsbyjs.org/). Here are some places to start:

- **For most developers, we recommend starting with our [in-depth tutorial for creating a site with Gatsby](https://www.gatsbyjs.org/tutorial/).** It starts with zero assumptions about your level of ability and walks through every step of the process.

- **To dive straight into code samples, head [to our documentation](https://www.gatsbyjs.org/docs/).** In particular, check out the _Guides_, _API Reference_, and _Advanced Tutorials_ sections in the sidebar.

## 💫 Deploy

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/gatsbyjs/gatsby-starter-default)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/import/project?template=https://github.com/gatsbyjs/gatsby-starter-default)

<!-- AUTO-GENERATED-CONTENT:END -->
