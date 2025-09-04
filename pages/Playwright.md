parent:: [[E2E Testing]]
related:: [[Cypress]]
link:: https://playwright.dev/

- A tool for [[E2E Testing]] that allows to test web applications
-
- ## 📔 Learning
	- https://frontendmasters.com/courses/testing/playwright/
-
-
- ## Basic Example
	- ```js
	  import { test, expect } from '@playwright/test';
	  
	  test('example with Playwright', async ({ page }) => {
	    // navigate to the page
	    await page.goto('https://example.com/login');
	  
	    // check the page title
	    await expect(page).toHaveTitle('Example Login Page');
	  
	    // fill in the login form
	    await page.fill('input[name="username"]', 'myUsername');
	    await page.fill('input[name="password"]', 'myPassword');
	  
	    await page.click('button#login');
	  
	    await page.waitForNavigation();
	  
	    const welcomeMessage = await page.textContent('h1#welcome');
	    expect(welcomeMessage).toBe('Welcome, myUsername!');
	  
	    await page.click('button#logout');
	  
	    await expect(page).toHaveURL('https://example.com/login');
	  });
	  
	  ```