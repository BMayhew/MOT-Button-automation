# Ministry of Testing 30 Days of Tools - Challenge #21

Inspired by this [blog post](https://louisegibbstest.wordpress.com/2021/12/08/waiting-vs-sleeping-stop-wasting-time/) by Louise Gibbs, I clicked the [button](https://ministryoftesting.github.io/the-button/) with implicit waits with Playwright.

If you want to run this on your local machine, git clone the repo to local. In the main directory run the below command. This will install playwright dependencies on your machine.

```bash
npx playwright install
```

To run the script (this isn't really a test as I'm not making any assertions). Note: headed will open up browser for you to see the interactions nad hear the sounds.

```bash
npx playwright test --headed
```

If you want to run the script in the cloud got to [try.playwright.tech](https://try.playwright.tech/) and paste the below in the editor.

```
const playwright = require('playwright');

(async () => {
  for (const browserType of ['chromium']) {
    const browser = await playwright[browserType].launch();
    const context = await browser.newContext();
    const page = await context.newPage();
    await page.goto('https://ministryoftesting.github.io/the-button/');
    await page.screenshot({ path: `green-before-push.png` });
    await page.locator('#theButton').click();
    await page.screenshot({ path: `red-after-push.png` });
    await page.waitForSelector('img[src*="green"]')
    await page.screenshot({ path: `green-after-push.png` });
    await browser.close();
  }
})();
```
