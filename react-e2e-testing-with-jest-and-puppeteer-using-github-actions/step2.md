# The TODO app

In this tutorial we will be testing a simple React app that handles TODO items. The app only consists of four things:

- Header
- Input field
- Submit button
- A list of TODO items

In order to run the application we first need to install all of its dependencies. We have already specified its dependencies in the `package.json` file so we can just run `npm install`{{execute}} to install the modules.

When all modules have been successfully downloaded, the app can be started by running the `npm start`{{execute}} command. 

We can know view the app by going to the url: https://[[HOST_SUBDOMAIN]]-3000-[[KATACODA_HOST]].environments.katacoda.com/


## Functionality

Now that we have our app up and running we can test its functionality. There are two main functions: adding TODOS and removing TODOS. 

Adding TODOS is done by writing the thing TODO into the input field and then pressing the `Submit Query` button.

Removing TODOS is done just as easily by pressing the `X` on the TODO item you want to remove.

Please try adding and removing TODOs in order to get comfortable with the app.

## App design and file structure

The app was initialized using the command `npx create-react-app` which generates a single page React app which prompts the user to edit `index.js` to begin. This is a good starting point for most projects and adds lots of good metadata. For example, it adds a public folder organizing files with metadata such as logos, description of the app and a `robots.txt` file (used by search engine crawlers to gain info on the site).

The structure in the `src/` folder is initially flat with all files in the same folder. In order to gain more structure to the project, it has been refactored to use the Model-View-Presenter(MVP) design pattern.


