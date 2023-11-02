## NEXT.js

- Nextjs Pre-renders every page, there are two forms of pre-rendering
  1. Static Generation(Recommanded): The HTML is generated at **build time** and will be **reused** on each request.(good for CDN, faster load time)
  1. Server-side Rendering: The HTML is generated on each request
  <br>
- These two forms can hybrid together for better performance


## Concept 
<span>Server Components vs Client Components</span>
  - server components: 
    - run on server
    - primarily focus on handling data-fetching, business logic, server-side tasks
    - generate HTML and send it to client side, then HTML become interative after hydration
  - client components: 
    - traditional react components, client is responsible for HTML generation
    - handle UI rendering and interations (form, navigation, client-side routing)
<br>

<span>Basic routing:</span> nextjs uses a file-system based router when folderss are used to define routes. When a different page is needed, create a dir in the parent directory for that page
  - `app` directory is a reserved name represeting the root directory of the pages, `next.config.js` has `appDir: true`
    - previously was `pages`

    - `page.js/jsx/tsx` is used to make route segments <span>publicly</span> accessible.

    - `Layout.tsx` is applied to all the components in the same dir
      - For `app` dir, a root `layout` is **required** and **applied** to all routes, it  <span>must</span> define `<html>` and `<body>` tags.

    - `styles.module.css` can be created in dir and apply only to files in the same dir, but `globals.css` will apply to all files.

    - Dynamic route: dir name with brackets `[parameterName]`:
       - Dynamic Segments are passed as the `params` prop to `layout`, `page`, `route`, `generateMetadata` functions
        ```
        // if below is in app/blog/[slug]/page.tsx
        export default function Page({ params }: { params: { slug: string } }) {
          return <div>My Post: {params.slug}</div>
        } 

        // URL: /blog/a 
        // route: app/blog/a/page.tsx 
        // params: { slug: 'a' } 
        ```
  - `lib` diretory: personal reference, contains and exports the code to query data.

<span>File Conventions</span>(`xxx.js/jsx/tsx`):
  - `default`: ???

  - `error`: defines an error UI boundary in case of error, doesn't crash the rest of the app.
    - must use `use clinet` at the top, Error components **must** be Client Components

  - `layout`: UI component that shared between routes

  - `loading`: instant loading statse built on react `<Suspense>`

  - `page`: UI that is unique to a route

  - `route`: route handler allows for custom request handlers for a given route

  - Metadata files (two ways): **Config-based** Metadata & **File-based** Metadata
    - previously use `head` file is used to add metadata, now it uses Metadata API to define `<meta>` and `<link>` tags for improved SEO:
      - <span>Config-based Metadata</span> 
        ```
        import type { Metadata } from 'next'

        // export static metadata object in layout or page file
        export const metadata: Metadata = {
          title: 'Next.js',
        }

        // use dynamic generateMetadata function to fetch metadata
        export async function generateMetadata(): Metadata {
          return {
            title: 'Next.js',
          }
        }
        ```
      - <span>File-based Metadata</span>:
        - `favicon.ico`, `apple-icon` and `icon.jpg`
        - `opengraph-image.jpg` and `twitter-image.jpg`
        - `robots.txt`
        - `sitemap.xml`

<span>Components</span>
  - Font (see below)
  - `<Link>`: React component extends `<a>` tag to provide **prefetching** (only in productino mode) and **client-side navigation** between routes.
    ```
    import Link from 'next/link';
    
    ...
    <Link href="/dashboard">Dashboard</Link>
    ...
    ```
  - `<Image>`
  - `<Script>`
    
<span>Functions</span>: reserved functions for specific purposes
  - cookies
  - draftMode
  - fetch
  - generateImageMetadata
  - `generateMetadata`: See above file conventions
  <br>
  
  - `generateStaticParams`: used in combination with **dynamic route segments** to **statically** generate routes **in advance** at build time instead of on-demand at request time. (SSG)
    ```
    // in app/blog/[slug]/page.js
    // Return a list of `params` to populate the [slug] dynamic segment
    export async function generateStaticParams() {
      const posts = await fetch('https://.../posts').then((res) => res.json())
    
      return posts.map((post) => ({
        slug: post.slug,
      }))
    }
    
    // Multiple versions of this page will be statically generated
    // using the `params` returned by `generateStaticParams`
    export default function Page({ params }) {
      const { slug } = params
      // ...
    }
    ```
  <br>

  - headers
  - ImageResponse
  - NextRequest
  - NextResponse
  - `notFound`:  render the **not-found file** within a route segment as well as inject a `<meta name="robots" content="noindex" />` tag.
    - directly use with no need for `return`: `if (!data) notfound()`
    - throws a `NEXT_NOT_FOUND` error and **terminates** rendering of the route segment in which it was thrown.
    - `not-found file`: by default a server component that handle such errors by rendering a Not Found UI within the segment.
  - permanentRedirect
  - redirect
  - revalidatePath
  - revalidateTag
  - Server Actions
  - userParams
  - usePathname
  - useReportWebVitals
  - `useRouter`: 
  - useSearchParams
  - useSelectedlayoutSegment
  - useSelectedLayoutSegments
  <br>

<span>Optimization</span>
  - Font implement:
    ```
    import { Roboto } from '@next/font/google'

    const roboto = Roboto({ 
      subsets: ['latin'],
      weight: ['400', '700'],
      ...
    })

    export default function App({ Component, pageProps }: AppProps) {
      return (
        <main className={roboto.className}>
          <Component {...pageProps} />
        </main>  
      );
    }
    ```

<span>Fetching Data Recommandations</span>

  - Fetch data on the server (server component)
  - Fetch data in parallel
  - Fetch data when it is used: `fetch` requests are automatically **memoized** in React, so for the same `fetch` request across all pages, **only executes first time**, the rest will take from the first request.
    - only applies to the `GET` method in fetch requests.
    - only applies to the React Component tree
    - [These](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating#opting-out-of-data-caching) fetch requests will not be cached
  - Use Loading UI, Streaming and Suspense

<span>Revalidation</span>: purging the Data Cache and re-fetching the latest data, works both in SSR and SSG implementation
  - **Time-based Revalidation**: 
    - Per request basis: put `option` object in `fetch` as `{ next: { revalidate: 3600 }}` (as seconds)
    ```
    fetch('https://...', { next: { revalidate: 3600 } })
    ```
    - Per page basis: use route segment config options to export revalidate value that sets everything on this level: 
    ```
    // in layout/page/route file
    export const revalidate = false | 'force-cache' | 0 | number
    ```
  - **On-demand Revalidation**: revalidate data based on an event (e.g. form submission). This is useful when you want to ensure the latest data is shown as soon as possible. On-demand by path(`revalidatePath(url)`) or cache tag (`revalidateTag(tagName)`)
  <br>

<span>Route Segment Config:</span> 

## Things to address later:
1. How does `import styles from './page.module.css'` + `<main className={styles.main}>` work? what is module.css file?
  <br>

1. Does NEXT create its own server? How to implement on an existing server?
  <br>

1. SSR vs SSG vs ISR
  - **SSR**: server-side render
  - **SSG**: server-side generation
  - **ISR**: incremental static regeneration, adding **validation** (use static-generation on a per-page basis, without needing to rebuild the entire site)
  <br>

1. when use `npm run build` in next.js:
  - λ  (Server)  server-side renders at runtime (uses `getInitialProps` or `getServerSideProps`)
  - ○  (Static)  automatically rendered as static HTML (uses no initial props)
  - ●  (SSG)     automatically generated as static HTML + JSON (uses getStaticProps)
  <br>

1. Hydration: attaching event handlers and making the page interactive. 
<br>

1. How does fetch validation work in dynamica routes?
<br>

1. Web Workers API
<br>

1. MIME types (Multipurpose Internet Mail Extensions)
