### 1. Styling

- `Tailwind` and `CSS modules` are the two most common ways of styling Next.js applications.
- It is good practice to add `global.css` to the top-level component - `root layout`.
- `clsx` lib can be used to conditionally apply the classes.

 ### 2. Optimizing Fonts
 - `Cumulative Layout Shift` - metric used by Google to evaluate the performance and user experience of a website.
 - When use the `next/font module` Next.js downloads font files at build time and hosts them with other static assets, so there are no additional network requests for fonts.
 - By adding font to the <body> element, it will be applied throughout your application. 
 - Fonts can also be added to specific elements of the application.
 - `font-smoothing: antialiased` - the smoothed font looks slightly lighter in weight

 ### 3. Optimizing Images
 - `next/image` component to automatically optimize images.
 - It's good practice to set size of the images to avoid layout shift (automatically - using a `static import`; explicitly - including a `width` and `height` property; implicitly, by using `fill`).
 - Next.js prioritize the image for loading with `priority` property (can be specified for every page). This leads to meaningful boost in LCP.
 - To safely allow optimizing images, define a list of supported URL patterns in `next.config.js`.
 - The default loader `does not optimize SVG` images. It is recommended using the `unoptimized` prop when the src prop is known to be SVG. This happens automatically when src ends with ".svg".
 - To serve SVG images with the default Image Optimization API, set `dangerouslyAllowSVG` inside the next.config.js
 - `onLoad`, `onError` callback functions can be used with Client Components.
 - Images are optimized dynamically upon request and stored in the `<distDir>/cache/images` directory. The optimized image file will be served for subsequent requests until the expiration is reached. The cache status of an image can be determined by reading the value of the `x-nextjs-cache` (MISS, STALE, HIT) 

 ### 4. Layouts and Pages
- Next.js uses `file-system routing` where folders are used to create nested routes. Each folder represents a route segment that maps to a URL segment.
- Next.js allows you to colocate UI components, test files, and other related code with your routes. Only the content inside the page file will be publicly accessible.
- `layout.tsx` file to create UI that is shared between multiple pages.
- One benefit of using layouts is that on navigation, only the page components update while `the layout won't re-render`.

### 5. Navigating Between Pages
- Next.js automatically code splits the application by route segments. Splitting code by routes means that pages become isolated. If a certain page throws an error, the rest of the application will still work.
-In production, whenever <Link> components appear in the browser's viewport, Next.js automatically prefetches the code for the linked route in the background. 
- Next.js provides `usePathname() hook` that can be used to check the path.
	
### 6. Fetching Data
- In Next.js, you can create API endpoints using Route Handlers.
- When using React Server Components (fetching data on the server), it's possible to skip the API layer, and query the database directly.
- By default, Next.js applications use React Server Components, which are executed on the server.
- Server Components support promises.
- By default, Next.js prerenders routes to improve performance, this is called `Static Rendering`. So if your data changes, it won't be reflected in your dashboard.

### 7. Static and Dynamic Rendering

- With `static rendering`, data fetching and rendering happens on the server at `build time` or during `revalidation`.
- Benefits of static rendering: Faster Websites(cached content), Reduced Server Load, SEO.
- With `dynamic rendering`, content is rendered on the server for each user at `request time`.
- Benefits of dynamic rendering: Real-Time Data, User-Specific Content, Request Time Information.

### 8. Streaming

- Streaming is a data transfer technique that allows to break down a route into smaller "chunks".
- Each component can be considered a chunk.
- There are two ways you implement streaming: `loading.tsx` file - for page, with <Suspense> - for component.

### 9. Partial Prerendering
- Partial Prerendering is an experimental feature.
- Allows to render a route with a static loading shell, while keeping some parts dynamic.
- At build time (or during revalidation), the static parts of the route are prerendered, and the rest is postponed until the user requests the route.
- When using Suspense to wrap the dynamic parts of the route, Next.js will know which parts of the route are static and which are dynamic.

### 10. Route Groups 
- Allows to organize your route segments and project files into logical groups without affecting the URL path structure.
- A route group can be created by wrapping a folder's name in parenthesis: `(folderName)`.
- It's possible to create a different layout for each group by adding a layout.js file inside their folders.
- To create multiple root layouts, remove the top-level layout.js file, and add a layout.js file inside each route group.
- Navigating across multiple root layouts will cause a full page load (as opposed to a client-side navigation).