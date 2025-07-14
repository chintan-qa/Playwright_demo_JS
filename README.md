👤 Author
Chintan Bhatt
QA Automation Engineer


# 🔐 ParaBank UI Test Automation – Playwright Framework

This project is a demo automation framework built using [Playwright](https://playwright.dev/) for testing the [ParaBank demo banking application](https://parabank.parasoft.com/parabank/login.htm).

It is designed with industry-standard best practices for structure, maintainability, and continuous integration.

## 🚀 Features

✅ Automated UI testing using **Playwright**  
✅ **Page Object Model (POM)** architecture  
✅ Centralized **constants** for selectors and messages  
✅ Modular **data factory** for test data management  
✅ **GitHub Actions** integrated for CI/CD  
✅ Clear and scalable project structure  
✅ Custom assertions and smart URL handling

---
📁 Project  Folder Structure

.github/workflows/

-playwright.yml – GitHub CI/CD workflow file

constants/

-messages.js – Common constants (messages, selectors, URLs)

datafactory/

-userFactory.js – Data factory for generating dynamic test data

pageobjects/

-signin_object.js – Page Object Model class for Sign In page

tests/

-SignIn.spec.js – Sample test spec

playwright.config.js – Playwright configuration (baseURL, timeouts, etc.)

package.json – NPM dependencies and scripts

README.md – Project documentation

🛠 Tech Stack

- **Playwright** (JavaScript)
- **Node.js**
- **GitHub Actions** (for CI)
- **ParaBank** demo site


🧱 Design Pattern: Page Object Model (POM)

All page-specific locators and actions are defined inside `pageobjects/` for maintainability.

Example: signin_object.js  
javascript
class SignInPage {
  constructor(page) {
    this.page = page;
    this.usernameInput = page.locator('input[name="username"]');
    this.passwordInput = page.locator('input[name="password"]');
    this.loginButton = page.locator('input[type="submit"]');
    this.errorMessage = page.locator('p.error');
  }

  async visitURL() {
    await this.page.goto('/');
    await this.page.waitForLoadState('domcontentloaded');
    await expect(this.page).toHaveTitle('ParaBank');
  }

  async login(username, password) {
    await this.usernameInput.fill(username);
    await this.passwordInput.fill(password);
    await this.loginButton.click();
  }

  async verifyLoginError(expectedMsg) {
    await expect(this.errorMessage).toHaveText(expectedMsg);
  }
}

module.exports = SignInPage;


🔄 Constants
Example constants/messages.js:

js
Copy
Edit
module.exports = {
  LOGIN_FAILURE: 'Please enter a username and password.',
};
Usage in test:

js
Copy
Edit
const CONSTANTS = require('../constants/messages');
await signInPage.verifyLoginError(CONSTANTS.LOGIN_FAILURE);

🧪 Running Tests Locally
1. Clone the repository
git clone https://github.com/your-username/playwright-project.git
cd playwright-project

2. Install dependencies
npm install

3. Run tests
npx playwright test

4. View HTML report
npx playwright show-report


📌 Best Practices Followed
✅ Page Object Model (POM)

✅ No hard-coded values — uses constants

✅ Independent and reusable test methods

✅ Proper waits and assertions

✅ Clean and minimal code structure

✅ GitHub Actions for CI/CD


