## E2E testing

It is perhaps easy to believe that because our application works purely code-wise in our immediate environment, that everything is peace and joy. However, we can probably not really be sure that our application works perfectly if a user would use it.
It is very possible that problems may arise that we do not really cover with our two previous tests.

**This is where E2E tests come in handy!**

Like metioned before in this tutorial, the main purpose of E2E tests is to test the **functionality and performance** of an application under product-like circumstances. The main goal is to as much as possible, simulate what a potential user scenario would look like from the start to finish.  
What is importante to mention as well is that there is a difference between having a system that **works** and having a system that behaves as it should.

So, to be able to test user flows within a web-application such as ours, we need to run our application on a webbrowser. For this, we will be using **Puppeteer**, a Node library which provides a high-level API to control Chrome over the DevTools protocol.

That might be loads of new words.. Let's be more concrete :)

- **node library**: Node.js and Javascript is hopefully something you already know much about, as a developer..
- **high-level API**: a human-readable interface for interacting with webpages through a brower (in our case Chrome).
- **DevTools Protocol** the standard protocol used in Chrome's functionalities.

## Puppeteer code

I think the easiest way to explain how Puppeteer works is by showing. So let's get into it!

Lets start by open our new testing file: Open `./react-e2e-testing/src/index.puppeteer.test.js`{{open}}

**Cool!**, now lets add a skeleton.

<pre class="file" data-filename="/root/react-e2e-testing/src/index.puppeteer.test.js" data-target="replace">
const puppeteer = require("puppeteer");
const URL = "http://localhost:3000/";


#E2E-test1



</pre>

Now let's add two E2E tests!

<pre class="file" data-filename="/root/react-e2e-testing/src/index.puppeteer.test.js" data-target="insert"  data-marker="#E2E-test1">

describe("First site", () => {
   test("Milk is in list", async () => {
    const browser = await puppeteer.launch({
      headless: true,
      args: ["--no-sandbox", "--disable-setuid-sandbox"],
    });
    const page = await browser.newPage();
    await page.goto(URL, { waitUntil: "domcontentloaded" });
    const text = await page.evaluate(() => document.body.textContent);
    expect(text).toContain("Milk");
    expect(text).toContain("Chocolate");
    await browser.close();
  }, 40000);


  #E2E-test2

});
</pre>

and:

<pre class="file" data-filename="/root/react-e2e-testing/src/index.puppeteer.test.js" data-target="insert"  data-marker="#E2E-test2">

 test("Add an element in shopping List", async () => {
    const browser = await puppeteer.launch({
      headless: true,
      args: ["--no-sandbox", "--disable-setuid-sandbox"],
    });
    const page = await browser.newPage();

    await page.goto(URL, { waitUntil: "domcontentloaded" });
    await page.waitForSelector("input[name=inputDiv]");
    await page.type("#katacodaid", "Eggs");
    await page.click("#clickbutton");

    const text = await page.evaluate(() => document.body.textContent);

    expect(text).toContain("Eggs");
    await browser.close();
  }, 40000);
</pre>

Now, open a new terminal! Open `cd ./react-e2e-testing/src/`{{execute T3}} .  
Now Open `cd react-e2e-testing/`{{execute T3}} .  
Before we run our tests, lets install all necessary stuff needed!
Lets start by running `sudo apt-get install -y libxkbcommon-x11-0`{{execute T3}} , make sure your localhost:3000 is active!

Now, lets run `npm test`{{execute}} and see what happens!
Hopefully you passed your (first?) E2E test! Congratulations!

## Lets talk about the code..

Our first E2E test:

- **describe** : Describe creates a block where we can group tests that are related.
- **it**: This is just and alias of **test** which we talked about before.
- **puppeteer.launch(..)**: Puppeter launches Chromium (Chrome).

  - **headless: true, args: ["--no.sandbox"]**: headless: true means that puppeteer uses no graphical user interface in this test. "No sandbox" is a security flag for websites.

- **.newPage()** creates a new page object. Page is created in a default browser context.

- **page.goto(URL)** Navigates to the given URL.

- **page.evaluate()** A page-funcation that evaluates the context in the actual page.

- **expect(text).toContain("Milk")** - expect is a Jest-function which gives you access of "matchers". In this case, we want a text to contain the word "Milk".

Our second E2E test is a bit different. In this test, we add a new element to the Shopping list and then checks that it actually appears on the screen. Lets go through the new methods.

- **waitForSelector("input[name=inputDiv]")** waits for the input with name = "inputDiv" appears on the page.
- **type("#katacodaid", "Eggs")** Types the text "Eggs" into the input with id="katacodaid", which is the input for our shopping list.- **click("#clickbutton")** Clicks the button which adds the element in the input to the list.
- **expect(..)** - last step checks if "Eggs" now is added to the list.

## What's next?

Nice!
What would it be like if we always made sure that our app fulfills these functions in the future? Can we somehow make sure that we always test this while building on our application?
