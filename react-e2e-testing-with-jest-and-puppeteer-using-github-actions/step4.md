# Testing in React

Now it's time to make make our first E2E test in React! Woho!

Like metioned before in this tutorial, the main purpose of E2E tests is to test the **functionality and performance** of an application under product-like circumstances. The main goal is to as much as possible, simulate what a potential user scenario would look like from the start to finish.  
What is importante to mention as well is that there is a difference between having a system that **works** and having a system that behaves as it should.

We will now write some code to test the functionality of our TODO-list.

```
test('test 2 buttons render', () => {
    render(<App />)
const buttons = screen.getAllByRole('button')
expect(buttons).toHaveLength(2)
})
```
