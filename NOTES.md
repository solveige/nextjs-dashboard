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
	