# Atlas
WP Engine's Atlas Headless Framework. This is a tutorial where we start from nothing. This does not include node.js installs though. Check out the Atlas Github repo [here](https://github.com/wpengine/headless-framework)

1. [If you're a dev, checkout our quickstart guide](https://github.com/KamabokoDesign/atlas-quickstart)

### Step 1
1. Create a new Next.js app from our getting-started project: `npx create-next-app -e https://github.com/wpengine/headless-framework/tree/canary --example-path examples/getting-started --use-npm`
1. `cd my-app`
1. `cp .env.local.sample .env.local`
1. `code .`
1. `npm run dev` to start the development server.
1. See your site at http://localhost:3000.

### Step 2
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

### Step 4
1. Dev vs. Production mode
1. `npm run build` will build the site statically
1. `npm start` will be on `localhost:8080` 
1. So open up your `localhost:8080` and bask in the beauty of React SPA. 

## Dissecting the WPEngine Next.js theme
We'll be taking a look into various files within the Next.js template

## [[...page]].tsx
This is the catch all page. The WP backend will send a client to this page first. 

## Creating a WP Independent Page (i.e. Hardcoded Pages)
1. Pages > New > authors.tsx
1. Add this code in authors.tsx
```
const AuthorsPage = () => {
  return <h1>Authors</h1>
}

export default AuthorsPage;
```
1. Go to page `localhost:3000/authors` should work

## Grabbing data from GraphQL
1. See the WP specifics here
2. But you can do something like this, in say an authors.tsx page:

```
import {useQuery, gql} from "@apollo/client";

const authorsQuery = gql`
 {
  users {
   nodes {
    avatar {
     url
    }
    firstName
    lastName
    roles {
     nodes {
     displayName
     }
    }
   }
  }
 }`;
 
 const AuthorsPage = () => {
  const {data} useQuery(authorsQuery);
  const authors = data?.users?.nodes ?? [];
  
  return (
  <>
  <div>
   <h1>Authors Page!</h1>
   <ol>
    {authors.map((author: any) => (
     <li>
      <img src={author.avatar.url} alt="" />
      <p>{author.firstName} {author.lastName}</p>
     </li>
    ))}
   </ol>
  </div>
  </>);
 }
 
 export default AuthorsPage;
 ```
 
 ## useGeneralSettings hook
 Another thing that WP Engine has built out is the useGeneralSettings hook. 
 
 1.  `import {useGeneralSettings} from @wpengine/headless/react`; 
 2.  `const settings = useGeneralSettings();`
 3.  To display info from that, you can also put


## To make your own pages

 ```
 export async function getStaticProps(context: GetStaticPropsContext) {
  const client = getApolloClient(context);
  client.query({
    query: authorsQuery
  })
  return getNextStaticProps(context);
 }
 ```
