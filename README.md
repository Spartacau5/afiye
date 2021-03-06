# afiye

---

## Installation

Fork this repository to your account.

Clone the forked repository to your device using a git GUI or the command line.

Navigate to the repository on the command line

```bash
cd path/to/repository
```

Install project dependencies

```bash
npm install
```

Create a `.env` file in the main directory of the repository.

## Database Installation and Initialization

### Neo4j

#### Neo4j Desktop

Download and install Neo4j Desktop for your OS from the [Neo4j Downloads page](https://neo4j.com/download/?ref=try-neo4j-lphttps://neo4j.com/download/?ref=try-neo4j-lp)

#### Database Initialization

Open Neo4j Desktop.

In the center panel click the `Add` button and select `Local DBMS` from the drop down options.

Name the database. This is just for your reference and will not be meaningful within the application.
*Recommended names for organization:* `afiye` or `afiye-main`

Set a database password. This can be anything (strong passwords are not necessary for local development), but note it for later.

From the version drop down select `4.2.2`. At time of writing, this is the latest version.

Create and start the database.

Make sure the database is selected in the list and select the the details tab. Copy the Bolt port, by default this is `bolt://localhost:7687`.

Add the following variables to your `.env` file.

```none
N4J_HOST=bolt://localhost:7687
N4J_USER=neo4j
N4J_PASS=abcde
```

*Notes:* `N4J_HOST` will be whatever is listed in the details panel in Neo4j Desktop. `N4J_USER` defaults to `neo4j` and should not be changed. `N4J_PASS` will be whatever you set it to during the database setup.

*Optional:* Back in the main Neo4j Desktop window rename the project for organizational purposes by hovering over the name (default `Neo4j Primer Project`) in the center panel and clicking the edit icon.

### MongoDB

#### Install MongoDB

##### MacOS

Follow the instructions [here](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/). Installing via Homebrew will install all the required binaries for this project, particularly the `mongo shell`.

##### Windows

Download MongoDB Community Server using the `msi` package option from the [Mongo Download Center](https://www.mongodb.com/try/download/community?tck=docs_server).

#### Database Initialization

##### MacOS

Start the [mongo shell](https://docs.mongodb.com/manual/mongo/).

From the command line:

```bash
mongo
```

Create a new database called `afiye`:

```bash
db afiye
```

Close the mongo shell with `ctrl + c`

##### Windows

Open MongoDB Compass.

On the *New Connection* panel press *CONNECT* **without typing anything in the 'Paste your connection string..' box** this will connect you to the default localhost environment `localhost:27017`.

Next, at the top of the main panel press *CREATE DATABASE* with the 'Database Name' set to 'afiye' and the 'Collection Name' set to 'users'.

##### All OS

Add the following to your `.env` file:

```none
MONGO_HOST=mongodb://localhost/afiye
```

## Mail Services Initialization

Add the following variables to your `.env` file. These are required to get your local version of this project running. Otherwise you will not be able to setup test user accounts. If you are directly working on Afiye, please contact project members for variable values, otherwise substitute with values for your application.

*Note:* For `MAIL_DOMAIN` for local development set the PORT portion of the variable to the aaplication port. See **Run Application** below for more information.

```none
MAIL_SERVICE_HOST=***********
MAIL_SERVICE_PORT=***********
MAIL_USER=***********
MAIL_PASS=***********
MAIL_DOMAIN=http://localhost:PORT
```

## Run Application

From the command line run the following command to open a development server. This will not generate any files on your system as they are saved into memory.

> **IMPORTANT:** Make sure all databases have been initialized and are running.

```bash
npm run buildDev && npm start
```

If you recieve an error messsage stating that a process is already running on `port 8080` add a `PORT` variable to your `.env` file. Recommended configuration:

```none
PORT=3000
```

## Test Build Application

*Recommended that* `NODE_ENV` *be set to* `production` *in your* `.env`

From the command line run the following command to build the project. This will populate the `dist` directory with the browser ready project files.

```bash
npm run buildProd
```

## Contribution Guidelines

### Code Best Practices

| Category | Description | Example |
| -------- | ----------- | ------- |
| File Naming | Use camelcase | `someFile.js` |
| `.scss` partials | Prefix with `_` | `_buttons.scss` |
| `scss` variables, classes, etc. | Separate words with `-` | `.some-class` |
| `js` variables, functions, etc. | Use camecase | `const submitMember` |

Use two space indents in all code files. This can be configured in your editor.

Preceed every `js` function with a comment describing its usage.

If `html` content will be dynamically added via `js` add a comment within the container element stating what will be added and by what function(s) to easily track.

Do not include links or references to `css` or `js` files in `html` files as they will be dynically added at build time with hash naming to avoid cache issues.

Any new `scss` partials must be included in `styles.scss` or it will not be compiled.

**DO NOT** touch anything in the Webpack folder unless you explicitly know what you are doing or have a hankering for a headache. Trust me. You will break it and we will all be sad.

Anything that should be included in the build must be included in the `src` directory or a subdirectory therein.

Please let Erik know if you are including a new file type in the build as this must be added to the build process.

Currently supports:

- EJS
- JS
- SCSS
- PNG
- JPEG
- GIF
- SVG
- WOFF
- WOFF2
- EOT
- TTF

### Pull Requests

All edits must be made in a forked version of this repository and submitted via a Pull Request (PR). Each PR must request a minimum of one reviewer, preferably one working on the same or a similar topic to the contents of your PR.

Prior to submitting a PR, ensure that your forked version has been synced with the latest version of the master repository to minimize merge conflicts. For information about syncing your repository please see the following:

- [GitHub Desktop](https://stackoverflow.com/questions/46110615/how-to-sync-your-forked-repo-with-original-repo-in-github-desktop)
- [Command Line](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork)

Every PR must be appropriately named. The title should reference the feature or bug being addressed by the changes. The description should provide an overview of changes and should be written in clear language that defines terms being used unless previously defined in project documentation.

### Approvals

Before a PR can be approved, reviewers must clone the changes to their machine and thoroughly test the build for any bugs. Any bugs should be reported in the review and the PR sent back to the author for correction before it can be merged into the master repository.

If a build is unsuccessful, the PR will be rejected.

If the code contains any errors or warnings per the project linting tools, the PR will be rejected.

If the code does not adhere to the Code Best Practices outlined above, the PR will be rejected.
