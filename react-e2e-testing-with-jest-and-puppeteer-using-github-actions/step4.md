# Testing in React

Now it's time to make make our first E2E test in React! Woho!

Like metioned before in this tutorial, the main purpose of E2E tests is to test the **functionality and performance** of an application under product-like circumstances. The main goal is to as much as possible, simulate what a potential user scenario would look like from the start to finish.  
What is importante to mention as well is that there is a difference between having a system that **works** and having a system that behaves as it should.

`git clone https://github.com/lucianozapata/react-e2e-testing` {{execute}}

We will now write some code to test the functionality of our TODO-list.

Let first write a simple test which tests if the page simply has the text "Shopping list" in it.

```
test('Should render header', () => {
    render(<InputPresenter/>);
    const header = screen.getByText(/Shopping list/i);
    expect(header).toBeInTheDocument();
});
```

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
