# Testing in React

Now it's time to make make our first E2E test in React! Woho!

Like metioned before in this tutorial, the main purpose of E2E tests is to test the **functionality and performance** of an application under product-like circumstances. The main goal is to as much as possible, simulate what a potential user scenario would look like from the start to finish.  
What is importante to mention as well is that there is a difference between having a system that **works** and having a system that behaves as it should.
Normally, the complexity of an application is much more advanced than in this example. E2E tests usually test that all the parts in an applications works as intended, which could include how backend, databases and frontend works all together.

// Brors kod här nere
`git clone https://github.com/lucianozapata/react-e2e-testing`{{execute}}

If you yet haven't installed & run the application, do so by firstly run `cd react-e2e-testing/`{{execute}}
and then `npm install`{{execute}} followed by `npm start`{{execute}}.
This will run the application in your localhost on port 3000. Press the "Display port 3000" in the terminal to see the app!
//Brors kod här uppe

### Our first tests for the application

We will now write some code to test the functionality of our TODO-list.
Open `./react-e2e-testing/src/index.test.js`{{open}} or locate to this file in the terminal to see where all our of tests will be at.
As you can see, there is already a test here. It basically tests that the header "Shopping list" exists in your localhost 3000 as shown before. Lets add one more test!

<pre class="file" data-filename="/root/react-e2e-testing/src/index.test.js" data-target="append">
test("Milk & chocolate in shopping list", () => {
  render(<InputPresenter />);
  const elem1 = screen.getByText("Milk");
  const elem2 = screen.getByText("Chocolate");
  expect(elem1).toBeInTheDocument();
  expect(elem2).toBeInTheDocument();
});
</pre>

Let's analyze this.

- test() defines a test, followed by a string describing what the test is all about. In our case it's called "Milk & cholocate in shopping list", which checks just that.
- After the description of the test comes the anonomys function of the test
- `render(<InputPresenter/>)` renders the InputPresenter our environment.
- `screen.getByText("Milk")` is a function to find non-interactive elements with the specific text. Such elements could be divs and spans.
- `expect(elem1).toBeInTheDocument()` checks if the element is in the DOM Tree.

### Run the tests locally

Cool! Now we have two basic tests for our application. Lets try and see if they pass!
Run `cd react-e2e-testing/src/`{{execute T2}} followed by `npm test`{{execute T2}} and see the results!

If everything has done correctly you should be seeing a `Tests: 2 passed, 2 total` in you terminal. Amazing! You've now confirmed that the those tests works in your local environment!

**Can we now make sure that our application works if we would host this on the web? What you think?**
