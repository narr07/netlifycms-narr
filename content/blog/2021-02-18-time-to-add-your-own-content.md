---
createdAt: 2021-02-18
title: Time to add your own content
description: Remove all of the .md-files in the /content folder and go at it!
---
<!--StartFragment-->

# Nuxt

This guide will walk you through how to integrate Netlify CMS with Nuxt.

## [](https://www.netlifycms.org/docs/nuxt/#starting-with-create-nuxt-app)Starting With `create-nuxt-app`

Follow the instructions on the [Nuxt documentation](https://nuxtjs.org/guide/installation#using-code-create-nuxt-app-code-) for creating a new project, or run:

```bash

```

## [](https://www.netlifycms.org/docs/nuxt/#setting-up-netlify-cms)Setting Up Netlify CMS

### [](https://www.netlifycms.org/docs/nuxt/#add-the-netlify-cms-files-to-nuxt)Add the Netlify CMS files to Nuxt

In the `static/` directory, create a new directory `admin/`. Inside that directory you'll create two files, your `index.html` and a `config.yml`. Per the [Netlify CMS documentation](https://www.netlifycms.org/docs/add-to-your-site/), we'll set the content of `static/admin/index.html` to the following:

```html

```

For your `static/admin/config.yml` file, you can put in a basic starter config:

```yaml

```

You can build whatever collections and content modeling you want. The important thing to note is the `format: 'frontmatter'` value on each collection. This is important for consuming content in Nuxt with the [nuxt/content](https://content.nuxtjs.org/) module.

### [](https://www.netlifycms.org/docs/nuxt/#add-the-content-directory-to-nuxt)Add the `content/` directory to Nuxt

In your root directory, you can create a new directory `content/`. As you might guess, this is where our content will live. Your filesystem should look about like this, so far:

```bash

```

### [](https://www.netlifycms.org/docs/nuxt/#pushing-to-github)Pushing to GitHub

It's now time to commit your changes and push to GitHub. `create-nuxt-app` initializes Git automatically for you, so you only need to do:

```bash

```

### [](https://www.netlifycms.org/docs/nuxt/#deploying-with-netlify)Deploying With Netlify

Now you can go ahead and deploy to Netlify. Go to your Netlify dashboard and click **[New site from Git](https://app.netlify.com/start)**. Select the repo you just created. Under **Basic build settings**, you can set the build command to `npm run generate` . Set the publish directory to `dist`. Click **Deploy site** to get the process going.

### [](https://www.netlifycms.org/docs/nuxt/#authenticating-with-netlify-identity)Authenticating with Netlify Identity

**Add the Netlify Identity Widget**

You've already added the Netlify Identity widget to our `admin/index.html`. The next thing to do is add the Netlify Identity widget to our site's index page. In `pages/index.vue`, we can add the following to the page `<script>` tag:

```javascript

```

Once you've added this, make sure to push your changes to GitHub!

*More on adding `<script>` tags to `<head>` [here](https://nuxtjs.org/faq/#local-settings).*

**Enable Identity & Git Gateway in Netlify**

Back in your [Netlify dashboard](https://app.netlify.com/):

1. Go to **Settings > Identity**, and select **Enable Identity service**.
2. Once enabled, select **Settings and usage**, and scroll down to **Registration preferences**. You can set this to either **Open** or **Invite only**, but usually **Invite only** is your best bet for a personal site.
3. If you don't want to create an account, or would like to use an external provider such as GitHub or Google, you can enable those services under **External providers**.
4. Scroll down to **Services** and click **Enable Git Gateway**.

**Accessing the CMS** Once you've reached this point, you should be able to access the CMS in your browser at `http://localhost:3000/admin`. You'll be prompted to add the URL of your Netlify site. Once you've added that URL, you can log in with an Identity account or with one of the External Providers you enabled in step 3 above. For the sake of this tutorial, you can create a blog post in the CMS, and publish it! Once you `git pull` in your project, the blog post will show up in the project at `content/blog/<slugified-blog-post-title>.md`.

## [](https://www.netlifycms.org/docs/nuxt/#using-nuxtcontent)Using nuxt/content

Netlify CMS and [nuxt/content](https://content.nuxtjs.org/) module click together and complement each other to give you best authoring experience and developer experience respectively.

Adding nuxt/content dependency

```javascript

```

Then, add @nuxt/content to the modules section of nuxt.config.js:

```javascript

```

By adding nuxt content module you get `$content` injected into your whole app which you can use to fetch content from your content folder using `simple fetch api` or `nuxt asyncData` option.\
This also gives a `<nuxt-content>` component which helps you display markdown content with ease and also gives option of live editing in dev mode.

### [](https://www.netlifycms.org/docs/nuxt/#example-blog-post-list)Example Blog Post List

nuxt/content module gives us $content which we can use to fetch the list of blog posts in content/blog directory.

![](/img/1ec2d8111703053.60155b77a0e9b.jpg)

### [](https://www.netlifycms.org/docs/nuxt/#example-blog-post)Example Blog Post

To generate blog posts create a `_slug.vue` file in the pages folder. By using `$content` you would get a json which you can use to display. But if you are using `markdown` to write and store your posts you can use `<nuxt-content>` module which gives you option to edit content on page in dev mode and many more [features](https://content.nuxtjs.org/).

```javascript

```

### [](https://www.netlifycms.org/docs/nuxt/#generating-pages-with-the-generate-property)Generating pages with the `generate` property

Since Nuxt 2.13+, nuxt export has a crawler feature integrated which will crawl all your links and generate your routes based on those links. Therefore you do not need to do anything in order for your dynamic routes to be crawled. i.e, if you are on version of nuxt above 2.14 add target as static in nuxt.config.js and use `nuxt generate` to build your static site.

```javascript

```

If you are using **nuxt version below 2.14** you have to use generate option in nuxt/content module to generate pages

```javascript

```

To render your site as a static site, you'll need to create or update the `generate` property in `nuxt.config.js` to create dynamic routes and provide their content as a `payload`. In `generate`, make your `routes` entry a function:

```javascript

```

To see the generated site, navigate to name-of-your-website.netlify.app/blog

<!--EndFragment-->