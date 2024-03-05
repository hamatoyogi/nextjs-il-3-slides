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
 src: ./2.md
---


---
src: ./3.md
---

---

## You might have something like this 👇🏽

```tsx {|2}
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


<!-- Both Route Handlers and Server Components run securely on the server. You don't need the additional network hop. Instead, you can call whatever logic you intended to place inside the Route Handler directly in the Server Component. This might be an external API or any Promise.
Since this code is running on the server with Node.js, we need to provide the absolute URL for the fetch versus a relative URL. In reality, we wouldn't hardcode localhost here, but instead need to have some conditional check based on the environment we're in. This is unnecessary since you can call the logic directly. -->

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

<!-- 
Show what happens locally vs prod
 -->

---
layout : center
---

### Understand local vs. production behavior and use dynamic fetching techniques when necessary.

---
layout: cover
---
# Unnecessary Route Handlers for Client Components

---

## Misconception that client components require separate route handlers.

### Use server actions for form submissions and interactions in client components.

---

# Using Suspense Incorrectly

## Misplacement of Suspense boundaries can lead to rendering issues.

### Place Suspense boundaries correctly to manage loading states and data fetching.

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
