---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
defaults:
  layout: center
transition: slide-left
title: Welcome to Slidev
mdc: true
monaco: true
monacoTypesSource: local # or cdn or none
layout: cover
---


# Fixing common mistakes in Next.js app router

---
transition: fade-out
layout: center
---

# Misusing Route Handlers



---
transition: fade-out
---

## Avoid unnecessary API calls in RSCs.


---

## You might have something like this 👇🏽

```ts {|4}
// app/api/data/route.ts

export async function GET(request: Request) {
  return Response.json({ data: 'Next.js' });
}
```

```tsx {|4}
// app/page.tsx

export default async function Home() {
  let res = await fetch('http://localhost:3000/api/data');
  let data = await res.json();

  return (
    <main className="...">
      <h2>{JSON.stringify(data)}</h2>;
    </main>
  );
}
```

<style>h2 { margin-bottom:2.5rem; }</style>


---
layout: center
class: text-center
---

 ## It works. but... 🤨
 ## <v-click>You don't need it 🤷🏽‍♂️</v-click>


---
class: why-not
---

# Why not?

<v-clicks>

- Route handlers and SC are already secure
- Extra network hop
- Need to provide absolute URL
- No easy place to add logic

</v-clicks>

<style>
  .why-not {
    h1 {
      color: hotpink;
    }
  }
</style>

---


# There's a better way!


---
class: direct
---

## <span v-mark.red="{ at: 1 }">Call async functions directly</span> or <span v-mark.red="{ at: 2 }">call external API directly</span>.


<div style="margin-bottom: 2rem;"></div>

````md magic-move
```tsx
export default async function Home() {
  let res = await fetch('http://localhost:3000/api/data');
  let data = await res.json();

  return (
    <main>
      <h1>{JSON.stringify(data)}</h1>
    </main>
  );
}

```
```tsx
export default async function Home() {
  // call your async function directly
  let data = await getData();

  return (
    <main>
      <h1>{JSON.stringify(data)}</h1>
    </main>
  );
}
```
```tsx
export default async function Home() {
  // or call an external API directly
  let data = await fetch('https://api.vercel.app/blog')

  return (
    <main>
      <h1>{JSON.stringify(data)}</h1>
    </main>
  );
}
```
````

---
layout: cover
---

# Misunderstanding Route Handler Defaults

---


## What will happen here?

<div style="margin-bottom: 2rem;" />

```ts {|5-7}
// src/app/api/date/route.ts

export async function GET() {
  return Response.json({
    time: new Date().toLocaleString('en-us', {
      timeZone: 'Asia/Jerusalem',
    }),
  });
}
```

<v-click at="2"><a href="http://localhost:3000/api/date" target="_blank">In action</a></v-click at="3">

<div style="margin-bottom: 2rem;" />

### <v-click at="3">Route handlers are cached by default, affecting dynamic data fetching.</v-click>


---
layout: center
---

### Understand local vs. production behavior  

<v-clicks>

  - Local dev handler is always dynamic
  - Prod will be static unless you access dynamic values

</v-clicks>

--- 

### Opting out of cache:

<div style="margin-bottom: 2rem;"/>

````md magic-move
```ts
// This is static

export async function GET() {
  return Response.json({
    time: new Date().toLocaleString('en-us', {
      timeZone: 'Asia/Jerusalem',
    }),
  });
}
```
```ts
// Any method besides GET makes it dynamic

export async function POST() {
  return Response.json({
    time: new Date().toLocaleString('en-us', {
      timeZone: 'Asia/Jerusalem',
    }),
  });
}
```
```ts
// use dynamic functions like cookies

import { cookies } from 'next/headers';

export async function GET() {
  const cookieStore = cookies()
  const theme = cookieStore.get('theme')
  return Response.json({
      theme
    }),
  });
}
```
```ts
// OR headers

import { headers } from 'next/headers'

export async function GET() {
  const headersList = headers();
  const referer = headersList.get('referer');
  return Response.json({
      referer
    }),
  });
}
```
```ts
// OR config route segments

// layout.tsx | page.tsx | route.ts

export const dynamic = 'auto'
export const dynamicParams = true
export const revalidate = false
export const fetchCache = 'auto'
export const runtime = 'nodejs'
export const preferredRegion = 'auto'
export const maxDuration = 5
 
export default function MyComponent() {}
```
````


---
layout: center
transition: fade-out
---

## One more workaround: `no-store`


---

```tsx {|4}
import { unstable_noStore as noStore } from 'next/cache';
 
export default async function Component() {
  noStore();
  const result = await db.query(...);
  ...
}
```

<div v-click style="margin-bottom: 2rem;"/>

## <span v-after>* this is still experimental</span>


---
layout: cover
---
# Unnecessary Route Handlers for Client Components

---

## <span v-click.hide at="1"> Client components don't need separate route handlers.</span>
## <span v-click at="1">Use server actions for form submissions and interactions in client components.</span>

<div style="margin-bottom: 2rem;"/>

````md magic-move
```tsx
'use client';

export default function Page() {
  const onSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    console.log('submit');
  };
  return (
    <main>
      <h2>Form</h2>
      <form onSubmit={onSubmit}>
        <button type="submit">Submit</button>
      </form>
    </main>
  );
}
```
```tsx
'use client'

import { send } from './actions';

export default function Page() {
  return (
    <main>
      <h2>Form</h2>
      <form action={send}>
        <button type="submit">Submit</button>
      </form>
    </main>
  );
}

// actions.ts

'use server';

export async function send() {
  console.log('sending from server!');
}
```
````

---

![Local Image](/bleeding-edge.jpeg)


---
class: text-center
transition: fade-out
---

# <a target="_blank" href="http://localhost:3000/use-optimistic">useOptimistic()</a>

## when using server actions


---

![Remote Image](https://i.imgflip.com/8i5idd.jpg)

---
transition: fade-out  
---

````md magic-move
```tsx
async function BlogPosts() {
  let data = await fetch('https://api.vercel.app/blog');
  let posts = await data.json();

  return (
    <ul>
      {posts.map((post: BlogPost) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

export default function Page() {
  return (
    <section className="w-full text-center pt-10">
      <h1 className="text-4xl mb-4">Blog Posts</h1>
      <BlogPosts />
    </section>
  );
}
```
```tsx
import { Suspense } from 'react';

async function BlogPosts() {
  let data = await fetch('https://api.vercel.app/blog');
  let posts = await data.json();

  return (
    <Suspense fallback={<div>loading...</div>}>
      <ul>
        {posts.map((post: BlogPost) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </Suspense>
  );
}

export default function Page() {
  return (
    <section className="w-full text-center pt-10">
      <h1 className="text-4xl mb-4">Blog Posts</h1>
      <BlogPosts />
    </section>
  );
}
```
````

---
transition: fade-out
---


![Remote Image](https://i.imgflip.com/8i5m83.jpg)


---
class: text-center
transition: fade
--- 

<h1>Right?!</h1>

---
class: text-center
--- 

## Misplacement of Suspense boundaries can lead to rendering issues.

<h2 v-click><a href="http://localhost:3000/suspense" target="_blank">👀</a></h2>


---
layout: two-cols
---

````md magic-move
```tsx
import { Suspense } from 'react';

async function BlogPosts() {
  let data = await fetch('https://api.vercel.app/blog');
  let posts = await data.json();

  return (
    <Suspense fallback={<div>loading...</div>}>
      <ul>
        {posts.map((post: BlogPost) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </Suspense>
  );
}

export default function Page() {
  return (
    <section>
      <h1>Blog Posts</h1>
      <BlogPosts />
    </section>
  );
}
```
```tsx
import { Suspense } from 'react';

async function BlogPosts() {
  let data = await fetch('https://api.vercel.app/blog');
  let posts = await data.json();

  return (
    <ul>
      {posts.map((post: BlogPost) => (
        <li key={post.id}>{post.title}</li>
      ))}
    </ul>
  );
}

export default function Page() {
  return (
    <section>
      <h1>Blog Posts</h1>
      <Suspense fallback={<div>loading...</div>}>
        <BlogPosts />
      </Suspense>
    </section>
  );
}
```
````

::right::

<div v-after style="height: 100%; display: grid; place-content: center; padding-left: 2rem;">
<h3>Place Suspense boundaries correctly to manage loading states and data fetching.</h3>
</div>

---

# Ignoring Request Information in Server Components

## Not utilizing request-specific information like headers or cookies in server components.

### Use built-in functionalities to access request information for more dynamic responses.

---

# Context Providers and Component Weaving

## Confusion over where to place context providers and how server and client components interleave.

### Proper placement of context providers and understanding the relationship between server and client components.

---

# Forgetting to Revalidate Data After Mutations

## Data inconsistencies after mutations due to lack of revalidation.

### Use caching strategies and revalidation techniques to ensure data consistency.

---

# Misplaced Redirects in Try/Catch Blocks

## Incorrect handling of redirects within try/catch blocks leading to errors.

### Place redirects appropriately to avoid catching redirect errors unintentionally.

---

# Conclusion

Recap of common mistakes and best practices to improve Next.js applications.
Encourage continuous learning and adaptation of best practices in Next.js development.
