# [Netlify-Dev](https://github.com/netlify/cli/blob/master/docs/netlify-dev.md#netlify-functions)

> Netlify Dev brings the power of Netlify's Edge Logic layer, serverless functions and add-on ecosystem to your local machine. It runs Netlify's production routing engine in a local dev server to make all **redirects, proxy rules, function routes or add-on routes** available locally and injects the correct environment variables from your site environment, installed add-ons or your netlify.toml file into your build and function environment.

![alt text](https://www.freecodecamp.org/news/content/images/2019/09/ASCCII-ART.png)

## :page_facing_up: 목차
* [Prerequisites](#prerequisites)
* [netlify.toml](#netlify.toml)
* [Redirects](#redirects)
* [Environment Variables](#environment-variables)
* [Netlify Functions](#netlify-functions)
* [Using Add-ons](#using-add-ons)


## Prerequisites
* You should have the latest Netlify CLI version. Run `npm install -g netlify-cli` to be sure.


## netlify.toml
`netlify.toml` file (in the project's root folder)   
```bash
# sample netlify.toml
[build]
  command = "yarn run build"
  functions = "functions" # netlify dev uses this to know where to scaffold and serve your functions
  publish = "dist"

# note: each of these fields are OPTIONAL
[dev]
  command = "yarn start" # Command to start your dev server
  port = 3000 # Port that the dev server will be listening on
  functionsPort = 34567 # port for functions server
  targetPort = 3000 # Port of target app server
  publish = "dist" # If you use a _redirect file, provide the path to your static content folder
  jwtRolePath = "app_metadata.authorization.roles" # Object path we should look for role values for JWT based redirects
  autoLaunch = true # a Boolean value that determines if Netlify Dev launches the local server address in your browser
  ```

## [Redirects](https://docs.netlify.com/routing/redirects/#syntax-for-the-redirects-file)
`_redirects` file (in the project's publish folder)

```bash
# Redirects from what the browser requests to what we serve
/home              /
/blog/my-post.php  /blog/my-post  
/news              /blog
/cuties            https://www.petsofnetlify.com
```

## Environment Variables
Netlify Dev supports local environment variables through .env files. Netlify Dev will look in project root directory and each of your JavaScript based Netlify Functions directories for .env file and will provide those variables to the spawned site generator/server and Netlify Functions.

## Netlify Functions
Netlify can also create serverless functions for you locally as part of Netlify Functions. The serverless functions can then be run by Netlify Dev in the same way that wold be when deployed to the cloud. :fire:

### usage
```bash
# Create a new function from one of the
# available templates offered when prompted (see below)
$ netlify functions:create

# alternatives
$ netlify functions:create hello-world # Create a new function with a given name
$ netlify functions:create --name hello-world # same

# Create a new function by cloning a template from a remote url
# organised with dependencies installed into a subdirectory
$ netlify functions:create hello-world --url https://github.com/netlify-labs/all-the-functions/tree/master/functions/9-using-middleware
```
### netlify functions:invoke
`netlify functions:invoke` allows you to locally test functions going above and beyond a simple GET request in browser. (we only model POSTs now but could easily expand from here).

```bash
# with prompting
netlify functions:invoke # we will prompt you at each step
netlify functions:invoke myfunction # invoke a specific function
netlify functions:invoke --name myfunction # invoke a specific function

# no prompting (good for CI)
netlify functions:invoke --name myfunction --identity # invoke a specific function with netlify identity headers
netlify functions:invoke --name myfunction --no-identity # invoke a specific function without netlify identity headers

# sending payloads
netlify functions:invoke myfunction --payload '{"foo": 1}'
netlify functions:invoke myfunction --querystring "foo=1"
netlify functions:invoke myfunction --payload "./pathTo.json"
```

### [netlify-lambda](https://github.com/netlify/netlify-lambda)
> Existing users of `netlify-lambda` should have no change to their workflow by switching to netlify dev. One immediate benefit is no need for proxying since `Netlify Dev` does that for you.


## [Using Add-ons](https://docs.netlify.com/partner-add-ons/get-started/)
Add-ons are a way for Netlify users to extend the functionality of their Jamstack site/app. :fire:   
```bash
 netlify addons:create fauna
 ```
 
[https://github.com/netlify/fauna-one-click](https://github.com/netlify/fauna-one-click)   

:arrow_forward: **Demo**: [https://epic-allen-669d8a.netlify.com](https://epic-allen-669d8a.netlify.com)

:memo: **참고 자료**   
[https://www.youtube.com/watch?v=RL_gtVZ_79Q&feature=youtu.be&t=812](https://www.youtube.com/watch?v=RL_gtVZ_79Q&feature=youtu.be&t=812)   
[https://www.youtube.com/watch?v=FMhVXOA54x8](https://www.youtube.com/watch?v=FMhVXOA54x8)   
[https://functions-playground.netlify.com/](https://functions-playground.netlify.com/)   
[https://functions.netlify.com/examples/](https://functions.netlify.com/examples/)   
[https://docs.netlify.com/cli/get-started/#get-help](https://docs.netlify.com/cli/get-started/#get-help)   
[https://scotch.io/tutorials/netlify-dev-the-power-of-netlify-on-your-local-computer](https://scotch.io/tutorials/netlify-dev-the-power-of-netlify-on-your-local-computer)   
   
:arrow_up: [위로 이동](#netlify-dev)

