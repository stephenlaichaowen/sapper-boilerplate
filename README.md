# Sapper boilerplate

What is Sapper ? It is a framework that combines Svelte and backend functionality(pulka or express) with SSR(Service Side Rendering) support, equivalent to Nuxt(Vue), Next(React). It allows developers to create dazzling full-stack web app with friendly SEO(Search Engine Optimization) support without hassle 

The default [Sapper](https://github.com/sveltejs/sapper) template, available for Rollup and webpack.

### Install Sapper 
Because there is something wrong with rollup, so we choose webpack version to make it work
```
npx degit "sveltejs/sapper-template#webpack" my-app
```

Then change directory to my-app, your project must be child folder or the compiler won't find it !!!
```
cd my-app
```

Install the dependencies 
```
npm i
```

Start the dev server
```
npm run dev
```

Open another terminal and run this command
```
npm run watch:tailwind
```

🛎️ If you want to upload static website(without backend services) in Netlify, Github Pages, or Firebase Hosting, please run `npm run build:tailwind` first to generate `index.css`, which is a purged css file and will be placed in the `__sapper__\export` directory; Then run `npm run export` to generate static files !!!

🛎️ If you want to upload your full-stack app(with backend services) in heroku, simply run `git push heroku master` to automatically build and deploy your app in heroku. You don't run `npm run build` to generate production ready files because the compiler will give you error messages !!!

### Install Tailwind 

Tailwind is ready to use out of box, but in case if you want to manually install in your newly created sapper project, you should follow the steps to complete.

Install Tailwind and postcss-cli
```
npm install tailwindcss postcss-cli --D
```

Remove unused styles, add PurgeCSS
```
npm install @fullhuman/postcss-purgecss
```

Create your Tailwind config file
```
npx tailwind init tailwind.js
```

Create a `postcss.config.js` file and add this to it
```
const tailwindcss = require("tailwindcss");

// only needed if you want to purge
const purgecss = require("@fullhuman/postcss-purgecss")({
  content: ["./src/**/*.svelte", "./src/**/*.html"],
  defaultExtractor: content => content.match(/[A-Za-z0-9-_:/]+/g) || []
});

module.exports = {
  plugins: [
    tailwindcss("./tailwind.js"),

    // only needed if you want to purge
    ...(process.env.NODE_ENV === "production" ? [purgecss] : [])
  ]
};
```

Next, create a CSS file for your Tailwind styles. You have to store in it static folder `static/tailwind.css` and add this to it :
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Install cross-env, dotenv
```
npm cross-env dotenv
```

Create `.env` under root directory and place this command
```
NODE_ENV=production
```

Update your `package.json` with the custom scripts.
```
"scripts": {
  "watch:tailwind": "postcss static/tailwind.css -o static/index.css -w",
  "build:tailwind": "cross-env NODE_ENV=production postcss static/tailwind.css -o static/index. css" ,
  "build": "npm run build:tailwind && sapper build"
}
```

Finally, add a stylesheet link to your `src/template.html` file
```
<link rel="stylesheet" href="index.css" />
```

## Deploy your Sapper App to cloud hosting services

### Deploy to Netlify

If your app doesn't need backend functionality, your site can be hosted and served as static files, which allows your site to be deployed to more hosting environments (such as Netlify, Firebase or Github Pages)

Generate production ready static files, and will be placed under `__sapper__\export` directory
```
npm run export
```

You can drag and drop `__sapper__/export` folder to deploy your site in 'Sites' tab of your Netlify account

or you can push your local project to remote git repo and upload to Netlify
- Go to 'app.netlify.com/teams/yourname/site'
- click 'New site from Git' button
- Under 'Continuous Deployment: GitHub App' select project in the list or type project name in search box then click the project link
- Under 'Deploy settings for yourname/projectname' enter `npm run export` (skip this step if you already run `npm run export` locally)
- Enter `__sapper__/export` in 'Publish directory' input box, then click 'Deploy site' button

### Deploy to Firebase Hosting

First you need to install firebase cli tools
```
npm i -g firebase-tools
```

Login to your firebase account(you can skip this step if you are already login)
```
firebase login
```

If something goes wrong, logout your firbase account then login again
```
firebase logout
```

Initialize firebase in your project, this will connect your local project to your firebase account
```
firebase init
```

Press `Enter` to select 'Hosting: Configure and deploy Firebase Hosting sites' 

Press `SPACE` to select your firebase project

Enter `__sapper__\export` as your public directory(When you build `sapper` project a `__sapper__\export` directory with procution-ready files will be generated and will overwrite this folder)

Create a `__sapper__\export` folder with production-ready build
```
npm run export
```

Test your site locally before deploy to firebase
```
firebase serve
```

Finally deploy your project to fireabse hosting
```
firebase deploy
```

### Deploy static files to Firebase Hosting

Most steps are the same as 'Deploy Sapper project to Firebase Hosting' except that you don't need to build your project for productin-ready, you simply choose `public` as your public directory and then place all static files in this folder 


### Deploy to Heroku

If your sapper app contains backend functionality, you have to deploy your app to Heroku hosting.

Make sure you have created a local git repo and update to latest commit
```
git init
git add .
git commit -m your-commit-message
```

Login your heroku account, this step is optional if you're already logged in
```
heroku login
```

Creating an app in your heroku account
```
heroku create
```

push your git master branch to heroku(Heroku will take care of build process under the hood)
```
git push heroku master
```

Open your app in browser
```
heroku open
```
  
If you don't like the name heroku generated automatically, you can rename your app from cli
```
heroku apps:rename newname
```

However if you rename your app in heroku page, you have to update your app name from cli
```
git remote rm heroku
heroku git:remote -a newname
```
# Sapper boilerplate

What is Sapper ? It is a framework that combines Svelte and backend functionality(pulka or express) with SSR(Service Side Rendering) support, equivalent to Nuxt(Vue), Next(React). It allows developers to create dazzling full-stack web app with friendly SEO(Search Engine Optimization) support without hassle 

The default [Sapper](https://github.com/sveltejs/sapper) template, available for Rollup and webpack.

### Install Sapper 
Because there is something wrong with rollup, so we choose webpack version to make it work
```
npx degit "sveltejs/sapper-template#webpack" my-app
```

Then change directory to my-app, your project must be child folder or the compiler won't find it !!!
```
cd my-app
```

Install the dependencies 
```
npm i
```

Start the dev server
```
npm run dev
```

Open another terminal and run this command
```
npm run watch:tailwind
```

🛎️ If you want to upload static website to Netlify, Github Pages, or Firebase Hosting, please run `npm run build:tailwind` first to generate `index.css`, which is a purged css file and will be placed in the `__sapper__\export` directory; Then run `npm run export` to generate static files !!!

🛎️ If you want to upload production build to Heroku, you don't run `npm run build`, because it will cause compiler errors; instead you run heroku-cli to build and deploy to heroku. To deploy your app in heroku, see the below instrouctions !!!

### Install Tailwind 

Tailwind is ready to use out of box, but in case if you want to manually install in your newly created sapper project, you should follow the steps to complete.

Install Tailwind and postcss-cli
```
npm install tailwindcss postcss-cli --D
```

Remove unused styles, add PurgeCSS
```
npm install @fullhuman/postcss-purgecss
```

Create your Tailwind config file
```
npx tailwind init tailwind.js
```

Create a `postcss.config.js` file and add this to it
```
const tailwindcss = require("tailwindcss");

// only needed if you want to purge
const purgecss = require("@fullhuman/postcss-purgecss")({
  content: ["./src/**/*.svelte", "./src/**/*.html"],
  defaultExtractor: content => content.match(/[A-Za-z0-9-_:/]+/g) || []
});

module.exports = {
  plugins: [
    tailwindcss("./tailwind.js"),

    // only needed if you want to purge
    ...(process.env.NODE_ENV === "production" ? [purgecss] : [])
  ]
};
```

Next, create a CSS file for your Tailwind styles. You have to store in it static folder `static/tailwind.css` and add this to it :
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Install cross-env, dotenv
```
npm cross-env dotenv
```

Create `.env` under root directory and place this command
```
NODE_ENV=production
```

Update your `package.json` with the custom scripts.
```
"scripts": {
  "watch:tailwind": "postcss static/tailwind.css -o static/index.css -w",
  "build:tailwind": "cross-env NODE_ENV=production postcss static/tailwind.css -o static/index. css" ,
  "build": "npm run build:tailwind && sapper build"
}
```

Finally, add a stylesheet link to your `src/template.html` file
```
<link rel="stylesheet" href="index.css" />
```

## Deploy your Sapper App to cloud hosting services

### Deploy to Netlify

If your app doesn't need backend functionality, your site can be hosted and served as static files, which allows your site to be deployed to more hosting environments (such as Netlify, Firebase or Github Pages)

Generate production ready static files, and will be placed under `__sapper__\export` directory
```
npm run export
```

You can drag and drop `__sapper__/export` folder to deploy your site in 'Sites' tab of your Netlify account

or you can push your local project to remote git repo and upload to Netlify
- Go to 'app.netlify.com/teams/yourname/site'
- click 'New site from Git' button
- Under 'Continuous Deployment: GitHub App' select project in the list or type project name in search box then click the project link
- Under 'Deploy settings for yourname/projectname' enter `npm run export` (skip this step if you already run `npm run export` locally)
- Enter `__sapper__/export` in 'Publish directory' input box, then click 'Deploy site' button

### Deploy to Firebase Hosting

First you need to install firebase cli tools
```
npm i -g firebase-tools
```

Login to your firebase account(you can skip this step if you are already login)
```
firebase login
```

If something goes wrong, logout your firbase account then login again
```
firebase logout
```

Initialize firebase in your project, this will connect your local project to your firebase account
```
firebase init
```

Press `Enter` to select 'Hosting: Configure and deploy Firebase Hosting sites' 

Press `SPACE` to select your firebase project

Enter `__sapper__\export` as your public directory(When you build `sapper` project a `__sapper__\export` directory with procution-ready files will be generated and will overwrite this folder)

Create a `__sapper__\export` folder with production-ready build
```
npm run export
```

Test your site locally before deploy to firebase
```
firebase serve
```

Finally deploy your project to fireabse hosting
```
firebase deploy
```

### Deploy static files to Firebase Hosting

Most steps are the same as 'Deploy Sapper project to Firebase Hosting' except that you don't need to build your project for productin-ready, you simply choose `public` as your public directory and then place all static files in this folder 


### Deploy to Heroku

If your sapper app contains backend functionality, you have to deploy your app to Heroku hosting.

Make sure you have created a local git repo and update to latest commit
```
git init
git add .
git commit -m your-commit-message
```

Login your heroku account, this step is optional if you're already logged in
```
heroku login
```

Creating an app in your heroku account
```
heroku create
```

push your git master branch to heroku(Heroku will take care of build process under the hood)
```
git push heroku master
```

Open your app in browser
```
heroku open
```
  
If you don't like the name heroku generated automatically, you can rename your app from cli
```
heroku apps:rename newname
```

However if you rename your app in heroku page, you have to update your app name from cli
```
git remote rm heroku
heroku git:remote -a newname
```
# Sapper boilerplate

What is Sapper ? It is a framework that combines Svelte and backend functionality(pulka or express) with SSR(Service Side Rendering) support, equivalent to Nuxt(Vue), Next(React). It allows developers to create dazzling full-stack web app with friendly SEO(Search Engine Optimization) support without hassle 

The default [Sapper](https://github.com/sveltejs/sapper) template, available for Rollup and webpack.

### Install Sapper 
Because there is something wrong with rollup, so we choose webpack version to make it work
```
npx degit "sveltejs/sapper-template#webpack" my-app
```

Then change directory to my-app, your project must be child folder or the compiler won't find it !!!
```
cd my-app
```

Install the dependencies 
```
npm i
```

Start the dev server
```
npm run dev
```

Open another terminal and run this command
```
npm run watch:tailwind
```

🛎️ If you want to upload static website to Netlify, Github Pages, or Firebase Hosting, please run `npm run build:tailwind` first to generate `index.css`, which is a purged css file and will be placed in the `__sapper__\export` directory; Then run `npm run export` to generate static files !!!

🛎️ If you want to upload your app with backend service to Heroku, you don't run `npm run build`, because it will cause compiler errors; instead you run heroku-cli to automatically build and deploy to heroku. To deploy your app in heroku, see the below instrouctions !!!

### Install Tailwind 

Tailwind is ready to use out of box, but in case if you want to manually install in your newly created sapper project, you should follow the steps to complete.

Install Tailwind and postcss-cli
```
npm install tailwindcss postcss-cli --D
```

Remove unused styles, add PurgeCSS
```
npm install @fullhuman/postcss-purgecss
```

Create your Tailwind config file
```
npx tailwind init tailwind.js
```

Create a `postcss.config.js` file and add this to it
```
const tailwindcss = require("tailwindcss");

// only needed if you want to purge
const purgecss = require("@fullhuman/postcss-purgecss")({
  content: ["./src/**/*.svelte", "./src/**/*.html"],
  defaultExtractor: content => content.match(/[A-Za-z0-9-_:/]+/g) || []
});

module.exports = {
  plugins: [
    tailwindcss("./tailwind.js"),

    // only needed if you want to purge
    ...(process.env.NODE_ENV === "production" ? [purgecss] : [])
  ]
};
```

Next, create a CSS file for your Tailwind styles. You have to store in it static folder `static/tailwind.css` and add this to it :
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Install cross-env, dotenv
```
npm cross-env dotenv
```

Create `.env` under root directory and place this command
```
NODE_ENV=production
```

Update your `package.json` with the custom scripts.
```
"scripts": {
  "watch:tailwind": "postcss static/tailwind.css -o static/index.css -w",
  "build:tailwind": "cross-env NODE_ENV=production postcss static/tailwind.css -o static/index. css" ,
  "build": "npm run build:tailwind && sapper build"
}
```

Finally, add a stylesheet link to your `src/template.html` file
```
<link rel="stylesheet" href="index.css" />
```

## Deploy your Sapper App to cloud hosting services

### Deploy to Netlify

If your app doesn't need backend functionality, your site can be hosted and served as static files, which allows your site to be deployed to more hosting environments (such as Netlify, Firebase or Github Pages)

Generate production ready static files, and will be placed under `__sapper__\export` directory
```
npm run export
```

You can drag and drop `__sapper__/export` folder to deploy your site in 'Sites' tab of your Netlify account

or you can push your local project to remote git repo and upload to Netlify
- Go to 'app.netlify.com/teams/yourname/site'
- click 'New site from Git' button
- Under 'Continuous Deployment: GitHub App' select project in the list or type project name in search box then click the project link
- Under 'Deploy settings for yourname/projectname' enter `npm run export` (skip this step if you already run `npm run export` locally)
- Enter `__sapper__/export` in 'Publish directory' input box, then click 'Deploy site' button

### Deploy to Firebase Hosting

First you need to install firebase cli tools
```
npm i -g firebase-tools
```

Login to your firebase account(you can skip this step if you are already login)
```
firebase login
```

If something goes wrong, logout your firbase account then login again
```
firebase logout
```

Initialize firebase in your project, this will connect your local project to your firebase account
```
firebase init
```

Press `Enter` to select 'Hosting: Configure and deploy Firebase Hosting sites' 

Press `SPACE` to select your firebase project

Enter `__sapper__\export` as your public directory(When you build `sapper` project a `__sapper__\export` directory with procution-ready files will be generated and will overwrite this folder)

Create a `__sapper__\export` folder with production-ready build
```
npm run export
```

Test your site locally before deploy to firebase
```
firebase serve
```

Finally deploy your project to fireabse hosting
```
firebase deploy
```

### Deploy static files to Firebase Hosting

Most steps are the same as 'Deploy Sapper project to Firebase Hosting' except that you don't need to build your project for productin-ready, you simply choose `public` as your public directory and then place all static files in this folder 


### Deploy to Heroku

If your sapper app contains backend functionality, you have to deploy your app to Heroku hosting.

Make sure you have created a local git repo and update to latest commit
```
git init
git add .
git commit -m your-commit-message
```

Login your heroku account, this step is optional if you're already logged in
```
heroku login
```

Creating an app in your heroku account
```
heroku create
```

push your git master branch to heroku(Heroku will take care of build process under the hood)
```
git push heroku master
```

Open your app in browser
```
heroku open
```
  
If you don't like the name heroku generated automatically, you can rename your app from cli
```
heroku apps:rename newname
```

However if you rename your app in heroku page, you have to update your app name from cli
```
git remote rm heroku
heroku git:remote -a newname
```
