---
theme: seriph
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
defaults:
  layout: center
transition: slide-left
title: Welcome to Next.js IL 3!
mdc: true
monaco: true
monacoTypesSource: local
author: Yoav Ganbar
layout: cover
---

# Common mistakes with App router and how to fix them

Tips and tricks for working with Next.js 14

<div class="uppercase text-sm tracking-widest">
Yoav Ganbar
</div>

<div class="abs-bl mx-14 my-12 flex">
  <img src="https://scontent.ftlv5-1.fna.fbcdn.net/v/t39.30808-6/347599427_6279683155482885_301452187387808483_n.png?stp=dst-jpg&_nc_cat=108&ccb=1-7&_nc_sid=5f2048&_nc_ohc=tGxFBTC-10IAX-axRtR&_nc_ht=scontent.ftlv5-1.fna&oh=00_AfBLPd2LkiUOXPJNOtt8UiJrqvBYRaxR7hBa7cnSNaFkmA&oe=65EDF281" class="h-8">
  <div class="ml-3 flex flex-col text-left">
    <div>Next.js IL Meetup #3</div>
    <div class="text-sm opacity-50">Mar. 6th, 2024</div>
  </div>
</div>

---
layout: 'intro'
---

# Yoav Ganbar

<div class="leading-8 opacity-80">
 DevRel & DX @ Builder.io<br>
 Father of 2.<br>
 Web dude, content creator & host of FedBites podcast.<br>
</div>

<div class="my-10 grid w-min gap-y-4" style="grid-template-columns: 40px 1fr;">
  <svg class="slidev-icon opacity-50" viewBox="0 0 24 24" width="1.2em" height="1.2em"><path fill="currentColor" d="M5.884 18.653c-.3-.2-.558-.455-.86-.816a50.59 50.59 0 0 1-.466-.579c-.463-.575-.755-.841-1.056-.95a1 1 0 1 1 .675-1.882c.752.27 1.261.735 1.947 1.588c-.094-.117.34.427.433.539c.19.227.33.365.44.438c.204.137.588.196 1.15.14c.024-.382.094-.753.202-1.095c-2.968-.726-4.648-2.64-4.648-6.396c0-1.24.37-2.356 1.058-3.292c-.218-.894-.185-1.975.302-3.192a1 1 0 0 1 .63-.582c.081-.024.127-.035.208-.047c.803-.124 1.937.17 3.415 1.096a11.73 11.73 0 0 1 2.687-.308c.912 0 1.819.104 2.684.308c1.477-.933 2.614-1.227 3.422-1.096c.085.013.158.03.218.05a1 1 0 0 1 .616.58c.487 1.216.52 2.296.302 3.19c.691.936 1.058 2.045 1.058 3.293c0 3.757-1.674 5.665-4.642 6.392c.125.415.19.878.19 1.38c0 .665-.002 1.299-.007 2.01c0 .19-.002.394-.005.706a1 1 0 0 1-.018 1.958c-1.14.227-1.984-.532-1.984-1.525l.002-.447l.005-.705c.005-.707.008-1.337.008-1.997c0-.697-.184-1.152-.426-1.361c-.661-.57-.326-1.654.541-1.751c2.966-.333 4.336-1.482 4.336-4.66c0-.955-.312-1.744-.913-2.404A1 1 0 0 1 17.2 6.19c.166-.414.236-.957.095-1.614l-.01.003c-.491.139-1.11.44-1.858.949a1 1 0 0 1-.833.135a9.626 9.626 0 0 0-2.592-.349c-.89 0-1.772.118-2.592.35a1 1 0 0 1-.829-.134c-.753-.507-1.374-.807-1.87-.947c-.143.653-.072 1.194.093 1.607a1 1 0 0 1-.189 1.045c-.597.655-.913 1.458-.913 2.404c0 3.172 1.371 4.328 4.322 4.66c.865.097 1.202 1.177.545 1.748c-.193.168-.43.732-.43 1.364v3.15c0 .985-.834 1.725-1.96 1.528a1 1 0 0 1-.04-1.962v-.99c-.91.061-1.661-.088-2.254-.485"></path></svg>
  <div><a href="https://github.com/hamatoyogi" target="_blank">hamatoyogi</a></div>
  <svg class="slidev-icon opacity-50" viewBox="0 0 24 24" width="1.2em" height="1.2em"><path fill="currentColor" d="M15.35 5.55a2.9 2.9 0 0 0-2.9 2.847l-.028 1.575a.6.6 0 0 1-.68.583l-1.562-.212c-2.053-.28-4.021-1.226-5.91-2.799c-.597 3.31.57 5.603 3.383 7.372L9.4 16.014a.6.6 0 0 1 .035.993L7.843 18.17c.947.059 1.846.017 2.592-.131c4.718-.942 7.855-4.492 7.855-10.348c0-.478-1.013-2.141-2.94-2.141m-4.9 2.81a4.9 4.9 0 0 1 8.385-3.355c.711-.005 1.316.175 2.668-.645c-.334 1.64-.5 2.352-1.213 3.331c0 7.642-4.697 11.358-9.464 12.309c-3.267.652-8.02-.419-9.38-1.841c.693-.054 3.513-.357 5.143-1.55c-1.38-.91-6.868-4.14-3.261-12.823c1.693 1.977 3.41 3.323 5.15 4.037c1.157.475 1.442.466 1.973.538"></path></svg>
  <div><a href="https://twitter.com/hamatoyogi" target="_blank">hamatoyogi</a></div>
  <svg class="slidev-icon opacity-50" viewBox="0 0 24 24" width="1.2em" height="1.2em"><path fill="currentColor" d="M20 22h-2v-2a3 3 0 0 0-3-3H9a3 3 0 0 0-3 3v2H4v-2a5 5 0 0 1 5-5h6a5 5 0 0 1 5 5zm-8-9a6 6 0 1 1 0-12a6 6 0 0 1 0 12m0-2a4 4 0 1 0 0-8a4 4 0 0 0 0 8"></path></svg>
  <div><a href="https://hamatoyogi.dev" target="_blank">hamatoyogi.dev</a></div>
</div>

<img src="/profile-pic.png" class="rounded-full bg-white w-40 abs-tr mt-16 mr-12"/>


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

![Local Image](/bleeding-edge-2.webp)


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

---

````md magic-move
```tsx
// app/page.tsx

export default function Page({
  params,
  searchParams,
}: {
  params: { slug: string };
  searchParams: { [key: string]: string | string[] | undefined };
}) {
  return <h1>My Page params {searchParams.hello}</h1>;
}
```

```tsx
// app/page.tsx

import { headers } from 'next/headers'
  export default function Page() {
  const headersList = headers()
  const referer = headersList.get('referer')
 
  return <div>Referer: {referer}</div>
}
```
```tsx
// app/page.tsx

import { cookies } from 'next/headers'
 
export default function Page() {
  const cookieStore = cookies()
  const theme = cookieStore.get('theme')
  return '...'
}
```
````


---
class: weave
layout: center
---

# Context Providers and Component Weaving

<img v-click src="https://1.bp.blogspot.com/-6FAZ8LiW-58/VqffUx_roxI/AAAAAAAAYHo/G7ItN6BGdJw/s1600/IMG_7648.JPG" style="height: 80vh; margin: auto;">

---

```tsx 
// app/theme-provider.tsx

'use client';

import { createContext } from 'react';

export const ThemeContext = createContext({});

export default function ThemeProvider({
  children,
}: {
  children: React.ReactNode;
}) {
  return <ThemeContext.Provider value="dark">{children}</ThemeContext.Provider>;
}
```

---

```tsx
// app/layout.tsx

import ThemeProvider from './theme-provider';

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html>
      <body>
        <ThemeProvider>{children}</ThemeProvider>
      </body>
    </html>
  );
}
```
---

# How to combine? 

---

## Server component

<div style="margin-bottom: 2rem;"></div>

```tsx 
// app/page.tsx

export default function Page() {
  return (
    <section>
      <h1>My Page</h1>
    </section>
  );
}
```

---
---

## Client component

<div style="margin-bottom: 2rem;"></div>

```tsx {|3|8}
// app/counter.tsx

'use client';

import { useState } from 'react';

export function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

---


````md magic-move
```tsx 
// app/page.tsx

export default function Page() {
  return (
    <section>
      <h1>My Page</h1>
    </section>
  );
}
```
```tsx 
// app/page.tsx

export default function Page() {

  return (
    <section>
      <h1>My Page</h1>
      <Counter />
    </section>
  );
}
```
```tsx
import { Counter } from './counter';

function Message() {
  return <p>This is a Server Component</p>;
}

export default function Page() {
  return (
    <section>
      <h1>My Page</h1>
      <Counter>
        <Message />
      </Counter>
    </section>
  );
}
```
```tsx
// app/counter.tsx

'use client';

import { useState } from 'react';

export function Counter({ children }: { children: React.ReactNode }) {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      {children}
    </div>
  );
}
```

````

---

# Don't “use client” unnecessarily

---

# Forgetting to revalidate data after mutations


---
transition: none
---

```tsx{|2-7}
export default function Page() {
  async function create(formData: FormData) {
    'use server';

    let name = formData.get('name');
    await sql`INSERT INTO users (name) VALUES (${name})`;
  }

  return (
    <form action={create}>
      <input name="name" type="text" />
      <button type="submit">Create</button>
    </form>
  );
}
```


---

````md magic-move
```tsx{|2-7}
export default function Page() {
  async function create(formData: FormData) {
    'use server';

    let name = formData.get('name');
    await sql`INSERT INTO users (name) VALUES (${name})`;
  }

  return (
    <form action={create}>
      <input name="name" type="text" />
      <button type="submit">Create</button>
    </form>
  );
}
```
```tsx
import { revalidatePath } from 'next/cache';

export default async function Page() {
  let names = await sql`SELECT * FROM users`;

  async function create(formData: FormData) {
    'use server';

    let name = formData.get('name');
    await sql`INSERT INTO users (name) VALUES (${name})`;

    revalidatePath('/');
  }

  return (
    <section>
      <form action={create}>
        <input name="name" type="text" />
        <button type="submit">Create</button>
      </form>
      <ul>
        {names.map((name) => (
          <li>{name}</li>
        ))}
      </ul>
    </section>
  );
}

```

````

---
layout: cover
---

# Misplaced Redirects

---

```tsx{|12}
import { redirect } from 'next/navigation';

async function fetchTeam(id) {
  const res = await fetch('https://...');
  if (!res.ok) return undefined;
  return res.json();
}

export default async function Profile({ params }) {
  const team = await fetchTeam(params.id);
  if (!team) {
    redirect('/login');
  }

  // ...
}
```

<!-- Don't return "redirect" -->

--- 
layout: full
---


```tsx{|3,7}
// app/client-redirect.tsx

'use client';

import { navigate } from './actions';

export function ClientRedirect() {
  return (
    <form action={navigate}>
      <input type="text" name="id" />
      <button>Submit</button>
    </form>
  );
}
```

```tsx{|8}
// app/actions

'use server';

import { redirect } from 'next/navigation';

export async function navigate(data: FormData) {
  redirect('/posts');
}
```

---
layout: center
---

# One more tip...

<Tweet v-click id="1758571101964382487" />


---


# Recap

<v-clicks>
  
  - Avoid unnecessary API calls in RSCs
  - Call things directly
  - Static Route handlers are cached by default
  - Behavior differs between dev / prod
  - Cache opt out methods
  - Handle form submissions with server actions
  - Put Suspense boundries in the right place
  - Remember what each page / route handler can access from a request
  - Learn how to knit server and client components
  - Don't “use client” unnecessarily
  - Revalidate data after mutations
  - Make sure to put redirects in the right place

</v-clicks>

---
layout: end
---

# Thank you!

<div class="my-10 grid w-min gap-y-4" style="grid-template-columns: 40px 1fr;">
  <svg class="slidev-icon opacity-50" viewBox="0 0 24 24" width="1.2em" height="1.2em"><path fill="currentColor" d="M5.884 18.653c-.3-.2-.558-.455-.86-.816a50.59 50.59 0 0 1-.466-.579c-.463-.575-.755-.841-1.056-.95a1 1 0 1 1 .675-1.882c.752.27 1.261.735 1.947 1.588c-.094-.117.34.427.433.539c.19.227.33.365.44.438c.204.137.588.196 1.15.14c.024-.382.094-.753.202-1.095c-2.968-.726-4.648-2.64-4.648-6.396c0-1.24.37-2.356 1.058-3.292c-.218-.894-.185-1.975.302-3.192a1 1 0 0 1 .63-.582c.081-.024.127-.035.208-.047c.803-.124 1.937.17 3.415 1.096a11.73 11.73 0 0 1 2.687-.308c.912 0 1.819.104 2.684.308c1.477-.933 2.614-1.227 3.422-1.096c.085.013.158.03.218.05a1 1 0 0 1 .616.58c.487 1.216.52 2.296.302 3.19c.691.936 1.058 2.045 1.058 3.293c0 3.757-1.674 5.665-4.642 6.392c.125.415.19.878.19 1.38c0 .665-.002 1.299-.007 2.01c0 .19-.002.394-.005.706a1 1 0 0 1-.018 1.958c-1.14.227-1.984-.532-1.984-1.525l.002-.447l.005-.705c.005-.707.008-1.337.008-1.997c0-.697-.184-1.152-.426-1.361c-.661-.57-.326-1.654.541-1.751c2.966-.333 4.336-1.482 4.336-4.66c0-.955-.312-1.744-.913-2.404A1 1 0 0 1 17.2 6.19c.166-.414.236-.957.095-1.614l-.01.003c-.491.139-1.11.44-1.858.949a1 1 0 0 1-.833.135a9.626 9.626 0 0 0-2.592-.349c-.89 0-1.772.118-2.592.35a1 1 0 0 1-.829-.134c-.753-.507-1.374-.807-1.87-.947c-.143.653-.072 1.194.093 1.607a1 1 0 0 1-.189 1.045c-.597.655-.913 1.458-.913 2.404c0 3.172 1.371 4.328 4.322 4.66c.865.097 1.202 1.177.545 1.748c-.193.168-.43.732-.43 1.364v3.15c0 .985-.834 1.725-1.96 1.528a1 1 0 0 1-.04-1.962v-.99c-.91.061-1.661-.088-2.254-.485"></path></svg>
  <div><a href="https://github.com/hamatoyogi" target="_blank">hamatoyogi</a></div>
  <svg class="slidev-icon opacity-50" viewBox="0 0 24 24" width="1.2em" height="1.2em"><path fill="currentColor" d="M15.35 5.55a2.9 2.9 0 0 0-2.9 2.847l-.028 1.575a.6.6 0 0 1-.68.583l-1.562-.212c-2.053-.28-4.021-1.226-5.91-2.799c-.597 3.31.57 5.603 3.383 7.372L9.4 16.014a.6.6 0 0 1 .035.993L7.843 18.17c.947.059 1.846.017 2.592-.131c4.718-.942 7.855-4.492 7.855-10.348c0-.478-1.013-2.141-2.94-2.141m-4.9 2.81a4.9 4.9 0 0 1 8.385-3.355c.711-.005 1.316.175 2.668-.645c-.334 1.64-.5 2.352-1.213 3.331c0 7.642-4.697 11.358-9.464 12.309c-3.267.652-8.02-.419-9.38-1.841c.693-.054 3.513-.357 5.143-1.55c-1.38-.91-6.868-4.14-3.261-12.823c1.693 1.977 3.41 3.323 5.15 4.037c1.157.475 1.442.466 1.973.538"></path></svg>
  <div><a href="https://twitter.com/hamatoyogi" target="_blank">hamatoyogi</a></div>
  <svg class="slidev-icon opacity-50" viewBox="0 0 24 24" width="1.2em" height="1.2em"><path fill="currentColor" d="M20 22h-2v-2a3 3 0 0 0-3-3H9a3 3 0 0 0-3 3v2H4v-2a5 5 0 0 1 5-5h6a5 5 0 0 1 5 5zm-8-9a6 6 0 1 1 0-12a6 6 0 0 1 0 12m0-2a4 4 0 1 0 0-8a4 4 0 0 0 0 8"></path></svg>
  <div><a href="https://hamatoyogi.dev" target="_blank">hamatoyogi.dev</a></div>
</div>