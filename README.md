# docker-auto-deploy

an nginx docker container to serve static files with auto-deploy functionality.

## Use case

you build a single page app using vue, react, etc. (or just basic html) and want to host it yourself. however, you don't want to juggle between your machine and your server to update the site (via `git pull`) everytime you push changes to your repo. this docker workflow does that `git pull` for you.

## Usage

1. clone or download the repo
2. put your static files inside `www` directory
3. run `docker-compose up`
4. set up a webhook that points to the endpoint of the `puller` (see: `docker-compose.yml` file)

## Demo

To make the usage more clear, let's demonstrate a scenario using github webhook.

1. fork this repo
2. clone your fork to your computer
3. once cloned, run `docker-compose up`
4. use `ngrok` to publish your puller service: `ngrok http 9999`
5. open your fork in github and go to **Settings** → **Webhooks** and click the "**Add Webhook**" button
6. key in your ngrok endpoint from step #4 in **Payload URL** column and save the setting
7. open `www/index.html` of your fork and edit it from github editor and save

at this point, github will send a request to your ngrok endpoint because the action you did in step #7 has triggered a push event. check your docker-compose logs and you'll see something like `pulling repo..`. 

now, check the `www/index.html` file in your local fork and you'll notice that it has been updated, just the same like what you updated from github editor. 

That's all! 
