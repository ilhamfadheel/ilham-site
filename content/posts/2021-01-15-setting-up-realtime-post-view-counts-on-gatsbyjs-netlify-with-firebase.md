---
template: SinglePost
title: Setting Up Realtime Post View Counts on GatsbyJS & Netlify with Firebase
status: Published
date: 2021-01-14
featuredImage: https://ucarecdn.com/9b64bc3e-73e6-4966-9320-5da257c3f67e/
excerpt: Setting Up Realtime Post View Counts on GatsbyJS with Firebase
categories:
  - category: Tech
---
Since my blog is a static site that doesn't have backend, I ran into the problem of not being able to track & show the view counts of my blog posts. By having view counts in my blog, it would help readers feels engaged and knows the worth of each of my posts.

So in this post I would like to show you the solution to tackle the problem by using Google Firebase's realtime database!

# Firebase Set up

1. Sign in to [Firebase](https://firebase.google.com/) and add new project. You can name it whatever you want.

![Start-Project](https://ucarecdn.com/ab100836-a01c-4564-8486-7d7d6d381344/ "Start Project")

2. Create a realtime database and choose the "start it test mode".
3. Next is to create a Web App in your Project Setting. Make sure to disable Firebase hosting and click on "Register app".

![Project Setting](https://ucarecdn.com/86e05eeb-2350-40a7-84c4-83218b49ce75/-/crop/912x290/0,0/-/preview/ "Project Setting")

![Project Setting](https://ucarecdn.com/a305a7e1-f034-49c1-a269-a449fb58a1c8/ "Project Setting")

4. Go to "Rules" in Realtime Database menu and set `read`, `write` to `true` and click on "Publish". this allow us to update data without signing in.

![](https://ucarecdn.com/ecd6eef0-0cc0-4f9c-b91f-34411a7a2be6/)

# Gatsby Set up

1. You need to install these 2 firebase dependencies inside your Gatsby Project. I use yarn for my package manager.

`yarn install firebase gatsby-plugin-firebase`  

2. Add the require dotenv at the top and gatsby-plugin-firebase inside your `gatsby-config.js`file.

> `gatsby-config.js`
>
> ```javascript
> require("dotenv").config({
>   path: `.env.${process.env.NODE_ENV}`,
> })
>
> module.exports = {
>   plugins: [
>     ...otherPlugins,
>
>     {
>       resolve: 'gatsby-plugin-firebase',
>       options: {
>         credentials: {
>           apiKey: process.env.GATSBY_API_KEY,
>           authDomain: process.env.GATSBY_AUTH_DOMAIN,
>           databaseURL: process.env.GATSBY_DATABASE_URL,
>           projectId: process.env.GATSBY_PROJECT_ID,
>           storageBucket: process.env.GATSBY_STORAGE_BUCKET,
>           messagingSenderId: process.env.GATSBY_MESSAGING_SENDER_ID,
>           appId: process.env.GATSBY_APP_ID,
>         },
>       },
>     },
>   ],
> };
> ```

3. create a `.env.development` file at the root of your gatsby site and have your previously made firebase credential values inside it. You can access these values again in your project setting under Web App.

> `.env.development`
>
> ```
> GATSBY_API_KEY='your_values_here'
> GATSBY_AUTH_DOMAIN='your_values_here'
> GATSBY_DATABASE_URL='your_values_here'
> GATSBY_PROJECT_ID='your_values_here'
> GATSBY_STORAGE_BUCKET='your_values_here'
> GATSBY_MESSAGING_SENDER_ID='your_values_here'
> GATSBY_APP_ID='your_values_here'
> GATSBY_MEASUREMENT_ID='your_values_here'
> ```

4. Since I'm using Netlify for my `.env.production / deployment environment` I need to put these values inside `environment variables` in my netlify settings as shown below. Different hosting has different settings be mindful for that. **NOTE: I forgot to add GATSBY\_ in front of all the variables in the pic. Gatsby requires GATSBY\_ naming convention for build .env variables as shown in this** [forum chat](https://community.netlify.com/t/how-to-access-environment-variables-in-a-react-component/1635/2).

![Netlify Setting](https://ucarecdn.com/8ff4ce4f-b9af-40fe-a30a-858aeb9f4096/ "Netlify Setting")

# Implementing the View Counts

1. Create a new file called `increment-views.js` inside a new `lib` folder inside your src and use the code below.

```
src
 | lib
    | increment-views.js
```

> `increment-views.js`
>
> ```
> import firebase from 'gatsby-plugin-firebase';
>
> const incrementViews = async (id) => {
>   const ref = firebase.database().ref(`/views`).child(id);
>
>   ref.transaction((currentViews) => {
>     return currentViews + 1;
>   });
> };
>
> export default incrementViews;
> ```

2. Create a new component file called `ViewCounter.js` inside your components folder and use the code below.

```
src
 | components
    | ViewCounter.js
```

> `ViewCounter.js`
>
> ```
> import React, { useEffect, useState } from 'react';
> import firebase from 'gatsby-plugin-firebase';
> import 'firebase/database';
> import incrementViews from '../lib/increment-views';
>
> const ViewCounter = ({ id }) => {
>   const [viewCount, setViewCount] = useState('');
>
>   useEffect(() => {
>     // 1 is displayed for a split second and then the correct count
>     // This is a workaround
>     const onViews = (newViews) => {
>       setViewCount(newViews.val() === 1 ? 0 : newViews.val());
>     };
>
>     incrementViews(id);
>
>     firebase.database().ref(`/views`).child(id).on(`value`, onViews);
>
>     return () => {
>       if (firebase.database()) {
>         firebase.database().ref(`/views`).child(id).off(`value`, onViews);
>       }
>     };
>   }, [id]);
>
>   return (
>     <div>
>       {viewCount ? viewCount : `---`} views
>     </div>
>   );
> };
>
> export default ViewCounter;
> ```

3. Now you can use ViewCounter component on the posts pages inside gatsby, here is how I use mine (I remove other code to make it easier to understand).

```
src
 | templates
    | SinglePost.js
```

> `SinglePost.js`
>
> ```
> import React, { Fragment } from 'react'
> import ViewCounter from '../components/ViewCounter';
>
> export const SinglePost= ({
>   slug
>   }) => (
>     <main>
>       <ViewCounter id={slug}/>
>     </main>
>  )
> export default SinglePost
> ```

# That's it !

Now every time someone visits your post, the view will be incremented. This is what it looks on my webpage and firebase's RTDB respectively. Hope you find this post useful, and if it is please leave a comment. Thanks for reading !

> My Blog Post with Views
>
> ![View Count](https://ucarecdn.com/d278c01a-f1b8-49a5-9ede-b3ff0909dc44/ "View Count")
>
> Firebase Database
>
> ![Firebase Views](https://ucarecdn.com/3adaac30-3073-414f-bf11-70f301dadf18/ "Firebase Views")