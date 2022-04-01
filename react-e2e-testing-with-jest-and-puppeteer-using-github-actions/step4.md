# Testing in React

// Brors kod här nere
`git clone https://github.com/lucianozapata/react-e2e-testing`{{execute}}

If you yet haven't installed & run the application, follow these steps:

- `cd react-e2e-testing/`{{execute}} , enter the correct folder.
- `npm install`{{execute}} . install all dependencies.
- `echo open new terminal 2`{{execute T2}} open a new terminal
- `cd react-e2e-testing/src/`{{execute T2}} enter the right folder in the new terminal
- `npm start`{{execute T2}}. run your application.
  This will run the application in your localhost on port 3000. Press the "Display port 3000" in the terminal to see the app!
  //Brors kod här uppe

### Our first tests for the application

We will now try to write our first React test for our TODO app!

Lets locate to the file where we will write our first test. Start with opening `./react-e2e-testing/src/index.test.js`{{open}} or locate to this file in the terminal.
As you can probably see, there is already a test here. What this simple test does is that it checks that it says "Shopping List" somewhere in our application, which it does.

Lets add a new test to our test-file!

<pre class="file" data-filename="/root/react-e2e-testing/src/index.test.js" data-target="append">
test("Milk & chocolate in shopping list", () => {
  render(<InputPresenter />);
  const elem1 = screen.getByText("Milk");
  const elem2 = screen.getByText("Chocolate");
  expect(elem1).toBeInTheDocument();
  expect(elem2).toBeInTheDocument();
});
</pre>

Interesting.. Let's analyze this new code.

- `test()` defines a test, followed by a string describing what the test is all about. In our case it's called "Milk & cholocate in shopping list", which checks just that.
- After the description of the test comes the anonomys function of the test
- `render(<InputPresenter/>)` renders the InputPresenter our environment.
- `screen.getByText("Milk")` is a function to find non-interactive elements with the specific text. Such elements could be divs and spans.
- `expect(elem1).toBeInTheDocument()` checks if the element is in the DOM Tree.

### Run the tests locally

Cool! Now we have two basic tests for our application. Lets try and see if they pass!
Run `cd react-e2e-testing/src/`{{execute T3}} followed by `npm test`{{execute T3}} and see the results!

If everything has done correctly you should be seeing a `Tests: 2 passed, 2 total` in you terminal. Amazing! You've now confirmed that the those tests works in your local environment!

Press **q** to exit the test results.

**Can we now make sure that our application works if we would host this on the web? What you think?**
