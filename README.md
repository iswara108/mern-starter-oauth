# MERN Starter by Jay Jay Cayabyab

This repository includes a boilerplate application that is designed as a launchpad for initializing boilerplate applications.

- The structure of the project in its current state assumes that the project will have two separate servers: one for the server-side and one for the client side.
- This starter assumes that you will be deploying to heroku and contains code that allows this to be done easily; however, this only pertains to the postbuild script inside of the `package.json` file. Otherwise, all other heroku-friendly changes are compatible with other deployment services.

## Table of Contents
1. [To-do before working on your project](#to-do-before-working-on-your-project)
2. [For heroku deployment](#for-heroku-deployment)
   - [For heroku initialization](#for-heroku-initialization)
   - [For consequent deployments](#for-consequent-deployments)
3. [Installed dependencies](#this-starter-installs-the-following-dependencies)
4. [Completed steps](#this-starter-automatically-completes-the-following-steps)

### To-do before working on your project:
- Edit the .gitignore file to include `dev.js`.
- Run the following code:
```
git rm --cached dev.js
npm i
cd client
npm i
```
- Delete the contents of this README.md and replace with `# {your-project-name}`.
- Add dev.js to your .gitignore file.
- Create a new MongoDB. mLab can be found [here](https://mlab.com/home).
- Generate new Google OAuth api keys [here](https://console.developers.google.com/).
- Update the keys in your `dev.js` file.

**For a separate github repo:**
- Run the following code:
```
git remote set-url origin {repo-url}
git add README.md
git commit -m "initial commit"
git push -u origin master
```

### For heroku deployment:

###### For heroku initialization:

- Ensure git is installed. Preferably, update the github repo with the instructions above.
- Ensure Heroku CLI is installed. You can download it [here](https://devcenter.heroku.com/articles/heroku-cli#download-and-install).
   - If not logged in, run `heroku login`.
- Run `heroku create`. This will log a git repository connected to heroku.
- Run
```
git remote add heroku {heroku git repository}
git push heroku master
```
- On heroku.com, navigate to settings.
- Add a MONGO_URI key-value pair in Config vars.
   - It would be preferred that this mongo database is unique from the development database.

###### For consequent deployments:
- Ensure that all files are saved and everything is committed
- Run
```
git push heroku master
```

#### This starter installs the following dependencies:

###### Server-side:
- Express
- Nodemon
- Concurrently
- Mongoose
- body-parser
- Passport.js
- Google Passport Strategy
- Cookie Session

###### Client-side:
- create-react-app dependencies
- Redux
- React-Redux
- Redux-Form
- Redux-Thunk
- axios

###### This starter automatically completes the following steps:
- Creates an Express app in index.js and initializes it to PORT 5000.
- Formats the package.json file:
   - Adds the *node* and *npm* engines for deployment purposes.
   - Creates two separate node instances on the back-end and the front-end.
   - Uses concurrently to run the entire application i.e. both the server and client node instances with `npm run dev`.
- Initializes a config folder with logic for prod vs. dev routing.
   - Provides key templates for `googleClientID`, `googleClientSecret`, `cookieKey`, and `mongoURI`.
- Hooks up body-parser middleware to Express application.
- Contains examples of Express routes, Mongoose models, and Express services.
- Sets up `Redux` logic around store and dispatch.
- Sets up `react-router` logic in `App.js`.
- Contains examples of Redux actions and reducers.
- Proxies HTTP requests from the front-end to the back-end server route `/api`.
- Handles authentication flow using Passport.js, CookieSession, and Google OAuth Strategy.
   - Creates some routes for handling authentication by the front-end:
   1. `/auth/google` for entering OAuth flow
   2. `/api/current-user` for return a JSON object of the current user
   3. `/api/logout` for logging the user out
   - Creates a "users" collection within the database.
     - This user has the following properties:
       - id: this is given by the OAuth service and is used to ensure there are no duplicate user documents.
       - firstName, lastName: contain the first and last name of the user.
   - Adds a requireLogin() middleware to be used within the backend to check if users are logged in before an HTTP request is made.
   - Passport makes the user available via the `req.user` object.