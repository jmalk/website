---
title: Why Use Layouts in NextJS
tags: til
---

# Why Use Layouts in Next

Next allows you to define a single shared layout for all pages with a [Custom App layout](https://nextjs.org/docs/basic-features/layouts#single-shared-layout-with-custom-app).

If you want different layouts for different pages, you'll need to use [Per-Page Layouts](https://nextjs.org/docs/basic-features/layouts#per-page-layouts). To do this, you add a `getLayout` function to your `Page` component. But the sample code puzzled me - it seems like a very roundabout way to pass a child component into a parent:

```
// pages/index.js

import Layout from '../components/layout'
import NestedLayout from '../components/nested-layout'

export default function Page() {
  return {
    /** Your content */
  }
}

Page.getLayout = function getLayout(page) {
  return (
    <Layout>
      <NestedLayout>{page}</NestedLayout>
    </Layout>
  )
}
```

Wouldn't it be simpler to do something like this?

```
// pages/index.js

import Layout from '../components/layout'
import NestedLayout from '../components/nested-layout'

export default function Page() {
  return (
    <Layout>
      <NestedLayout>
        /** Your content */
      </NestedLayout>
    </Layout>
  )
}
```

I found the answer in [this reddit thread](https://www.reddit.com/r/reactjs/comments/shyhd0/whats_the_point_of_getlayout_in_nextjs/). When you change pages on a Next site, everything inside the page re-renders. By specifying a separate Layout for pages, we can persist state and create a Single-Page App experience.

Writing this out leads me to another question though. If you have different layouts for different pages, presumably they still can't share state, and you must re-render when changing from one layout to another?