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
Let first write a simple test which tests if the page simply has the text "Shopping list" in it. Open `/root/react-e2e-testing/src/index.test.js`{{open}} to see it!

As you can see, there is already a test here. It basically tests that the header "Shopping list" exists in your localhost 3000 as shown before. Lets add one more test!

<pre class="file" data-filename="/root/react-e2e-testing/src/index.test.js" data-target="append">
test("Default shopping list is correct", () => {
  render(<InputPresenter />);
  const elem1 = screen.getByText("Milk");
  const elem2 = screen.getByText("Chocolate");
  expect(elem1).toBeInTheDocument();
  expect(elem2).toBeInTheDocument();
});
</pre>

Now, lets write a test that checks if the items "Chocolate" and "Milk" is a part of the shopping list.

```
test("Default shopping list is correct", () => {
  render(<InputPresenter />);
  const elem1 = screen.getByText("Milk");
  const elem2 = screen.getByText("Chocolate");
  expect(elem1).toBeInTheDocument();
  expect(elem2).toBeInTheDocument();
});
```
