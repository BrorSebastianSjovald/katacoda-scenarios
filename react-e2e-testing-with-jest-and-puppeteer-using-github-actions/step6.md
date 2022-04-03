## What is Github Actions?

Nice, you've come a long way already!
Now we know that our application does what it is supposed to, with the help of testing! But let's say that we want to continue to develop our app with new features, and that we may have several teams working on it at the same time, how do we ensure that we continuously check that no one's changes crash the app?
Well, we can do that with the help of **Github Actions!** Github actions is a continuous integration and continuous delivery (CI / CD) platform, which allows us to automate our tests and builds. CI is one of the most fundamental basics of DevOps.

## Why do we want to use Github Actions?

CI can save a lot of time due to its automation. By having a functioning, automated and stable pipeline, teams can save a lot of time by focusing on the important thing instead: developing a good product. Depending on how you use Github actions, you can by combining it with CI mergea code between different teams without creating major conflicts and be sure that everything works as intended.

## How do we use Github Actions workflow in our app?

In our app's repository, we create a `.github/workflows` directory. In this directory we now create _.yml_ - file. We can call it _node.js.yml_  
This will now be our **workflow file**. Depending on what you want to run / automate in the pipeline, you change it in this file. In our case, we run the following workflow:

<pre class="file">
name: Node.js CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [12.x, 14.x, 16.x]
        # See supported Node.js release schedule at https://nodejs.org/en/about/releases/

    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v2
        with:
          node-version: ${{ matrix.node-version }}
          cache: "npm"
      - run: npm ci
      - run: npm run build --if-present
      - run: npm start & npm test

</pre>

If we now commit this change to our Github Repository, we have the setup ready to use Github Actions.

We will now to through th _.yml_-file briefly, to get a better understanding of what this file actually does.

**name: Node.js CI -**

_Optional:_ The name of the workflow as it will appear in the Actions tab of the GitHub repository.

**on:**

Specifies the trigger for this workflow. This example uses the `push` & `pull_request` event, so a workflow run is triggered every time someone pushes a change to the repository or merges a pull request on the specified branch (**main** in our case)

**Jobs:**

Groups together all jobs run in our workflow.

**Build:**
Name of our job. The child keys will define the properties of the job.

**Runs on: ubuntu-latests**

Configures the job to be run on the latest ubuntu linux runner. This job will be run on a virtual machine hosted by Github.

**Strategy:**

This defines a build matrix for all of our jobs. Here we can specify if we want our jobs to be run with different configurations. In our case, we run it with 3 different node versions, 12.x, 14.x and 16.x.

**steps:**

Groups together all the steps that run in the **build** job.

**uses: actions/checkout@v2**

This is an action that checks out our repository onto the runner, allowing us to run scripts & other actions against our code. We will in our case use this to run our tests.

**uses: actions/setup-node@v2**

This step uses the actions/setup-node@v2 to install the specified node version we want, which in our case the ones defined in the matrix explained before.

**Run:**

The run keywords tells the job to execute the command on the runner. This is where we run **npm start & npm test** just as we did in our local environment.

## Github Actions feedback

That’s a lot of information! But it’s really not that complicated! By configuring this _.yml file_ as we want it to behave, we really make life easier for developers working on this repository.

_How do we get feedback if our tests actually passes or not ?_ - you may ask.  
Well, depending on the configuration in the _.yml file_, we can make Github inform us as soon as we push code into the repository. In our case, we let Github inform us as soon as we push or make a Pull_request on the main-branch.

Here under are some pictures on where to navigate to get to the Github Actions feature on Github, and see how a commit is pushed to the code and goes through the workflow. The last picture shows when Github actions returned that all tests had passed.

<iframe src="https://drive.google.com/file/d/1YDXIDRfhNDpMsRWjmCTDx9As7KZoR9jC/view?usp=sharing" width="640" height="480"></iframe>

<iframe src="https://drive.google.com/file/d/1OViCNnuMXO5XWam26ZWmTdfMfVARQuEg/view?usp=sharing" width="640" height="480"></iframe>

<iframe src="https://drive.google.com/file/d/1xNSD5XEcTICxOKpfsncLr-hymhl5KRdQ/view?usp=sharing" width="640" height="480"></iframe>

<iframe src="https://drive.google.com/file/d/1TtCxBBrKpT15Zk9alZHGavgVFDGgrs12/view?usp=sharing" width="640" height="480"></iframe>

<iframe src="https://drive.google.com/file/d/1NtoV7Yh4TkJjD4OECz--VODmCdFskYnD/view?usp=sharing" width="640" height="480"></iframe>
