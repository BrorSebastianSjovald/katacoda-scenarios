## E2E testing

It is perhaps easy to believe that because our application works purely code-wise in our local environment, that everything is peace and joy. However, a small part is missing for a complete testcoverage, which is how the application works in practice, ie when a user actually uses the application. It is very possible that things may appear here that are not completely covered by previous tests.
**This is where E2E tests come in handy!**

So, to be able to test user flows within a web-application such as ours, we need to run our application on a webbrowser. For this, we will be using **Puppeteer**, a Node library which provides a high-level API to control Chrome over the DevTools protocol.

That might be loads of new words.. Let's be more concrete :)

- **node library**: Node.js and Javascript is hopefully something you already know much about, as a developer..
- **high-level API**: a human-readable interface for interacting with webpages through a brower (in our case Chrome).
- **DevTools Protocol** the standard protocol used in Chrome's functionalities.

## Puppeteer code

I think the easiest way to explain how Puppeteer works is by showing. So let's get into it!

Lets start by open our new testing file: Open `./react-e2e-testing/src/index.puppeteer.test.js`{{open}}

**Cool!**, now lets add a code-skeleton

<pre class="file" data-filename="/root/react-e2e-testing/src/index.puppeteer.test.js" data-target="replace">
import { render, screen } from "@testing-library/react";
import { InputPresenter } from "./presenters/InputPresenter";
const puppeteer = require("puppeteer");
const URL = "http://localhost:3000/";

#E2E-test1

</pre>

Now let's add our first E2E test!

<pre class="file" data-filename="/root/react-e2e-testing/src/index.puppeteer.test.js" data-target="insert"  data-marker="#E2E-test1">

describe("First site", () => {
  it(" Milk is in list", async () => {
    const browser = await puppeteer.launch({
      headless: true,
      args: ["--no-sandbox"],
    });
    const page = await browser.newPage();
    await page.goto(URL, { waitUntil: "domcontentloaded" });
    const text = await page.evaluate(() => document.body.textContent);
    expect(text).toContain("Milk");
    expect(text).toContain("Chocolate");
  });
});
</pre>

Now, open a new terminal an go to Open `./react-e2e-testing/src/`{{open}}. Before we run our tests, lets install all necessary stuff needed!

Lets run `npm test`{{execute}} and see what happens!
Hopefully you paased your (first?) E2E test! Congratulations!

Lets talk about the code..

- **describe** : Describe creates a block where we can group tests that are related.
- **it**: This is just and alias of **test** which we talked about before.
- **puppeteer.launch(..)**: Puppeter launches Chromium (Chrome).

  - **headless: true, args: ["--no.sandbox"]**: headless: true means that puppeteer uses no graphical user interface in this test. "No sandbox" is a security flag for websites.

- **.newPage()** creates a new page object. Page is created in a default browser context.

- **page.goto(URL)** Navigates to the given URL.

- **page.evaluate()** A page-funcation that evaluates the context in the actual page.

- **expect(text).toContain("Milk")** - expect is a Jest-function which gives you access of "matchers". In this case, we want a text to contain the word "Milk".
