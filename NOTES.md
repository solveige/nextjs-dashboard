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