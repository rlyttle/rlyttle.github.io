---
title: "Angular 9 Bundle Size Analysis"
date: 2020-05-28T19:16:54+01:00
draft: false
---

<!-- ## Intro -->
I recently had to perform bundle analysis on an angular project to track down an issue causing increased bundle size, leading to improved efficiency of the app initialisation following optimisation of associated libraries and SCSS.


#### Install webpack-bundle-analyser
{{< highlight bash >}}
npm i webpack-bundle-analyzer --save-dev
{{< /highlight >}}

#### Build the angular project stats JSON
{{< highlight bash >}}
ng build --prod --stats-json
{{< /highlight >}}

#### Analyse the stats JSON
{{< highlight bash >}}
npx webpack-bundle-analyzer dist/<PROJECT-NAME>/stats.json
{{< /highlight >}}

This starts a web server locally providing a size analysis of different components within the angular bundle, as seen below

{{< figure src="/img/angular-bundle-analysis-1.png" alt="Hello Friend" position="center" style="border-radius: 10px; border: 1px solid #292929;" caption="" captionPosition="center" captionStyle="color: white;" >}}

This will give us ideas as to how to reduce the bundle size. E.g. do we need all those moment.js locales? Note that if you see a massive styles.scss file within the bundle, this may be due to a rogue SCSS loop generating an unexpected amount of CSS rules - each one increasing the styles.css file size. You may also notice some libraries no longer used by the project that you forgot to remove from package.json - removing anything unnecessary may reduce the bundle size significantly and lead to faster loading times.