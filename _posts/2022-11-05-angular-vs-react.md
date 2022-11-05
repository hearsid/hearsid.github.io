---
layout: post
title: "Angular VS React: Performance comparison with Google Web Vitals"
date:   2022-11-05 19:33:58 +0530
category: javascript
---

![](https://miro.medium.com/max/1155/1*BkoTJN4n5cQrgagMRUrEPg.png)

**Target Audience:**  
Software Developers/ Technical Managers who want to compare performance metrics of Angular and React to get better perspective about which one of these is more suitable for an upcoming project.

## **Introduction**

Angular is a JavaScript framework built by Google, while React is a Javascript library built by Facebook. Angular is mostly used to build complex CRUD applications quickly, while React makes it possible to build apps that need to show a lot of data and need frequent and fast data update with its virtual DOM concept.

This post is going to compare the performance difference between React and Angular in terms of:  
1) App bundle size (JS files only) 
2) Heap size
3) DOM nodes
4) DOM Content Loaded (DCL)
5) First Contentful Paint (FCP)
6) Largest Contentful Paint (LCP)
7) Time To Interactive (TTI)
8) Scripting time
9) Rendering time

We will be comparing the data from **Performance, Memory, Lighthouse, Performance insights (its still a preview feature) and Network tab** of Chrome Devtools for a simple application (Contact manager) created in both **React (v18.2.0)** and **Angular (v14.2.6)**.

## Contact Manager Application

![](https://miro.medium.com/max/1155/1*ZZIh7U5yecraVNNf36zeAQ.png)

Preview Contact Manager application

We are going to create Contact manager application in both React and Angular. Angular application was created using **Angular CLI** and React application using **Create React App (CRA)**. The application will have some contacts by default and will have option to increase number of contacts, to allow you to compare these with different number nodes. There is option to provide a **query parameter in the URL, no\_of\_contacts** so that we can dynamically provide the number of contacts to be generated. In this article, we will be looking at performance results for 1,000 contacts.

If you would like to check the application’s performance for a different set of contact number, the **applications can be accessed by the URL provided or cloned from Github repo link provided** at bottom of article.  
NOTE: I have tried to list most accurate readings but there are factors like latency and caching etc which could have affected them.

## **Table of readings (For 1,000 Contacts)**

## Setup Details

Hosting: Github pages  
Angular stack: Angular v14.2.6 with default packages.  
React stack: React (v18.2), react-router-dom, Typescript.

Lets dive in and see how the above reading were taken and how they contribute in enhancing the performance of our application.

## 1) Application Bundle Size

Application size decides the download time of the files by the browser and plays an important role, specially when the application size is very big or our target audience may be using slow internet connection. The pictures below are of the tab of chrome dev tools and the application size shown in the above table has been calculated by adding the JS file size. The file size can also be checked from the lighthouse report.

![](https://miro.medium.com/max/1155/1*JwHTHHJot8rF4X_ilkgsRQ.png)

1.1 Angular Contact manager network tab

![](https://miro.medium.com/max/1155/1*EV2VumPmFHu6ME4uc4wutw.png)

1.2 React Contact manager network tab

## 2) Heap size

Memory tab is going to show the memory distribution by the page’s JavaScript objects and related DOM nodes. Readings for both Angular and React look fine as for our application.

![](https://miro.medium.com/max/1155/1*JkqZgqgNgFM-nPfLCQd7YA.png)

2.1 Angular app heap snapshot

![](https://miro.medium.com/max/1155/1*bCM7WMyWtXmCfG6IlQIGuA.png)

2.2 React app heap snapshot

## 3) DOM nodes

This is crucial since a template parser’s internal compilation of the templates may result in the insertion of a few extra DOM nodes. Lesser the node elements, lighter the DOM tree, the better it is. But in our case the number of DOM nodes are same for Angular and React.

## 4) DCL- DOM Content Loaded

When the HTML document has been fully parsed and all deferred scripts have downloaded and run, the DOMContentLoaded event is fired. It doesn’t wait for other elements like as async scripts, subframes and pictures to finish loading. In the below screenshot and for comparison **best of 3 readings** been taken. We can take readings for these Web vitals from Performance and Lighthouse tab as well. The application looks like this or with less styling after DOM Content Loaded event.

![](https://miro.medium.com/max/521/1*59wAq9hNmLIeYIzShBPDfw.png)

4.1 Application after DCL

![](https://miro.medium.com/max/1155/1*pfNKKlS15P_TqbnZutwVFg.png)

4.2 Angular app DCL, FCP, TTI, LCP

![](https://miro.medium.com/max/1155/1*OH1AKAzSErOeuax9VeU-_A.png)

4.3 React app DCL, FCP, TTI, LCP

## 5) FCP- First Contentful Paint

First Contentful Paint (FCP) is when the browser renders the first bit of content from the DOM, providing the first feedback to the user that the page is actually loading. The appliation should looks like this after FCP.

![](https://miro.medium.com/max/518/1*Kbl5KHi3PSXbT-ALtZVqUg.png)

5.1 Application after FCP

## 6) LCP- Largest Contentful Paint

LCP measures the time from when the user initiates loading the page until the largest image or text block is rendered within the viewport.

## 7) TTI- Time To Interactive

The TTI metric measures the time from when the page starts loading to when its main sub-resources have loaded and it is capable of reliably responding to user input quickly. **Our application should be completely loaded after this.**

## 8) Scripting time

How much of the total time was spent in scripting phase by the framework. There is significant difference in this for Angular and React,

![](https://miro.medium.com/max/1155/1*O8Ia1niCDC73TiLSeH_bRQ.png)

4.1 Angular app Performance app

![](https://miro.medium.com/max/1155/1*ZQH8gN2eCY5D9efpT54vdg.png)

4.2 React app Performance tab

## 9) Rendering Time

How much of the total time was spent in the rendering phase by the frameworks.

## 10) Onload event

The load event is fired when the whole page has loaded, including all dependent resources such as stylesheets and images. This is in contrast to DOM Content Loaded event, which is fired as soon as the page DOM has been loaded, without waiting for resources to finish loading.

## Repository links:

-   [Angular Contact manager Github repository](https://github.com/hearsid/ng-contact-manager)
-   [React Contact manager Github repository](https://github.com/hearsid/react-contact-manager)

## Application links:

-   [Angular Contact manager application link](https://hearsid.com/ng-contact-manager/#/contacts?no_of_contacts=100)
-   [React Contact manager application link](https://hearsid.com/react-contact-manager/?no_of_contacts=100)