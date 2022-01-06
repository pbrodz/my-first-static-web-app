# Vanilla JavaScript App

[Azure Static Web Apps](https://docs.microsoft.com/azure/static-web-apps/overview) allows you to easily build JavaScript apps in minutes. Use this repo with the [quickstart](https://docs.microsoft.com/azure/static-web-apps/getting-started?tabs=vanilla-javascript) to build and customize a new static site.

This repo is used as a starter for a _very basic_ HTML web application using no front-end frameworks.

# Lessons learned when doing this (https://docs.microsoft.com/en-us/azure/static-web-apps/getting-started?tabs=vanilla-javascript)

0. Make sure you have the Azure Static Web Apps extension for VSC installed
1. Use a GitHub template repository that features a starter app used to deploy using Azure Static Web Apps. This will create the site in your GitHub repo
   https://github.com/login?return_to=/staticwebdev/vanilla-basic/generate
2. Clone to local
3. Locally in VSC, log into whichever Azure Sub you'll be deploying/doing the work using the Azure activity bar
4. Under "Static Web Apps" click the "+" and fill in the blanks. Choose "No Framework/Custom" and /src as the location for the application files. Build output location = ""
5. GitHub will now remote build the application and you can then run it by R-clicking on the "Production" node and hit "Browse Site"
6. You can add an API now for your site to hit as follows:
   a) Make sure you have the Azure Functions extension installed and the latest LTS version of Node.js
   b) F1 -> Azure Static Web Apps: Create HTTP Function...
   JavaScript
   c) Change the function as follows:
   module.exports = async function (context, req) {
   context.res.json({
   text: "Hello from the API"
   });
   };
   d) Update the SPA to call the API as follows:
   <!DOCTYPE html>
   <html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="styles.css">
    <title>Vanilla JavaScript App</title>
</head>

<body>
    <main>
    <h1>Vanilla JavaScript App</h1>
    <p>Loading content from the API: <b id="name">...</b></p>
    </main>

    <script>
    (async function() {
        const { text } = await( await fetch(`/api/message`)).json();
        document.querySelector('#name').textContent = text;
    }())
    </script>

</body>

</html>
e) Install Azure Static Web Apps CLI and Azure Functions Core Tools V3 to run all this locally for testing as follows:
npm install -g @azure/static-web-apps-cli
npm install -g azure-functions-core-tools@3
f) Run the following to start the app locally in order to test it:
swa start src --api-location api
g) Make sure you have the .yml have "api" for its "api_location" property set
h) git commit & push (cool you can do this from F1 also)
i) Go to the Actions section of GitHub to see the workflow run
j) Go to portal.azure.com and navigate to your now published site!
