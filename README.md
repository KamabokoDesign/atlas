# Atlas
WP Engine's Atlas Headless Framework. This is a tutorial where we start from nothing. This does not include node.js installs though. Check out the Atlas Github repo [here](https://github.com/wpengine/headless-framework)

1. [If you're a dev, checkout our quickstart guide](https://github.com/KamabokoDesign/atlas-quickstart)

## Step 1
1. Create a new Next.js app from our getting-started project: `npx create-next-app -e https://github.com/wpengine/headless-framework/tree/canary --example-path examples/getting-started --use-npm`
1. `cd my-app`
1. `cp .env.local.sample .env.local`
1. `code .`
1. `npm run dev` to start the development server.
1. See your site at http://localhost:3000.

## Step 2
1. Config the .env.local in the next.js
```
# Either WORDPRESS_URL or NEXT_PUBLIC_WORDPRESS_URL need to be populated. Not both!
#
# Setting WORDPRESS_URL instead of NEXT_PUBLIC_WORDPRESS_URL will limit requests to the WordPress backend
# to only come from the Node.js server.
#
# Setting NEXT_PUBLIC_WORDPRESS_URL instead of WORDPRESS_URL will allow requests to come from the client-side which may
# reduce site performance and put extra load on the WordPress backend.
#
# NOTE: In order for previews to work you must use NEXT_PUBLIC_WORDPRESS_URL

NEXT_PUBLIC_WORDPRESS_URL=http://localhost:8888/atlas-wp/
# WORDPRESS_URL=http://localhost:8888/atlas-wp/

# Plugin secret found in WordPress Settings->Headless
WP_HEADLESS_SECRET=YOUR_PLUGIN_SECRET (copy this from your WP Admin)
```

## Step 3
1. Make sure to redeploy your next.js localhost with `npm run dev`
1. In WP Admin > Pages > Add New > "Test Page" for example
1. Now you can go to `http://localhost:3000/test-page` and things should render


## Posts
WPEngine seems to have really mastered the Posts section of WP + Next integration. When you want to make a new post. You can preview it automatically in the Next.js build, and posts won't be public until you publish them! Yes and yes.

## Step 4
1. Dev vs. Production mode
1. `npm run build` will build the site statically
1. `npm start` will be on `localhost:8080` 
1. So open up your `localhost:8080` and bask in the beauty of React SPA. 