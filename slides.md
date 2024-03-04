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
  foo: true
transition: slide-left
title: Welcome to Slidev
mdc: true
monaco: true
monacoTypesSource: local # or cdn or none
---

# Fixing common mistakes in Next.js app router

---

# Misusing Route Handlers

---

## Avoid unnecessary API calls within React Server Components.

```ts
// app/api/data/route.ts

export async function GET(request: Request) {
  return Response.json({ data: 'Next.js' });
}
```

---

## You might have something like this 👇🏽

```ts
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

---

## It works. but... 🤨


---

## You don't need it 🤷🏽‍♂️

---

Solution: Directly call functions or fetch data without intermediate route handlers.

---

# Misunderstanding Route Handler Defaults

## Route handlers are cached by default, affecting dynamic data fetching.

### Understand local vs. production behavior and use dynamic fetching techniques when necessary.

---

# Unnecessary Route Handlers for Client Components

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
