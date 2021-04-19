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
1. Setup your WP container to run Wordpress locally
1. [Download and Install MAMP](https://www.mamp.info/en/downloads/)
1. Start up MAMP > Start > Should open in `localhost:8888` or `localhost`
1. Scroll down to MySQL or go to url `http://localhost:8888/phpMyAdmin/?lang=en`
1. Hit Databases > Create Database > Add a Database name > Name it the same thing as your next.js repo > Create


1. [You can download Wordpress here](https://wordpress.org/download/#download-install)
1. Applications > MAMP > htdocs > create a new folder, name it the same thing as your next.js repo
1. Open up your Wordpress download zip > open up the folder > select all files > copy > open up the MAMP wordpress htdocs folder
1. Open up your localhost at `http://localhost:8888/headlessnext` (headlessnext should be the name of your folder you put in the MAMP folder)
1. Choose your language
1. Database name should be the name of your next.js repo or the database you named in your Wordpress install
1. Username: root > Password: root > Database Host and Table Prefix keep default
1. Run the installation
1. Site title can be whatever you want
1. Username: root & Password: root
1. You in fam

## Step 3

1. Plugin installs
1. Install the `WPGraphQL` Wordpress Plugin & activate

The reason for favouring GraphQL is that it's faster than the REST API and GraphQL gives us the power and flexibility to return only the data we need. Using the WPGraphiQL plugins also allows us to both build our queries directly inside of our WordPress instance before moving them into Next.js. [Source](https://dev.to/kendalmintcode/configuring-wordpress-as-a-headless-cms-with-next-js-3p1o)

1. Install the [WPEngineHeadless plugin](https://wp-product-info.wpesvc.net/v1/plugins/wpe-headless?download)
1. Activate both plugins