# Digital Ocean Static App Deploy

First, if you haven't used Digital Ocean yet, [sign up for $100 credit](https://m.do.co/c/47e5e578d1cd).

Deploying your first three static sites is cost free on Digital Ocean. Your React applicatons are considered to be static apps, so you won't be charged for them, unless you go over your 3 free static deployed apps.

## Deploy Static Application

1. In Digital Ocean, create a new application. Do not make this part of your API app.
2. Connect Digital Ocean to your Github account if you haven't yet.
3. Click the Github icon.
4. Choose your repository from the search field that appears.
5. Click next.
6. It will auto-detect that you're trying to deploy a **Static Site** and all of the defaults should be unchanged. If it doesn't edit the project to change its type from **Web Service** to **Static Site**.
    > Note: If you get a message that it could not find an app in your repo, type `/src` in the "Source directory" field and click "Find directory".
7. Click next.
8. Type in an app name like "sinks-steve" or anything else that works.
9. Click next.
10. Make sure **Starter Plan** is chosen.
11. Click **Launch Starter App**.

Now wait for a few minutes while your application is built and deployed. Once successful, you can click on the link they provide and see your site!

## Updating API To Support New Client

1. Copy the new domain that your app is deployed to
2. Go to your API app on Digital Ocean.
3. Update the environment variables to update this one.

| Variable name | Value | 
|---|--|
| DJANGO_ALLOWED_HOSTS | ${APP_DOMAIN},localhost,127.0.0.1,&lt;new client domain name&gt; |

4. Then go to your API project in VS Code and open `settings.py`.
5. Find the `CORS_ORIGIN_WHITELIST` section.
6. Add a new entry in that tuple with the full URL to your new deployed client.
7. Add, commit, and push and wait for your API to deploy again.
