#  Selenium Automation 

## 🌐 Practice Sites for Automation
- [UltimateQA Automation](https://ultimateqa.com/automation)
- [SauceDemo](https://www.saucedemo.com/)
- [DemoQA](https://demoqa.com/)
- [GlobalSQA AngularJS Practice Site](https://www.globalsqa.com/angularjs-protractor-practice-site/)

---
---

##  Build automation tools

When we start automation testing using tools like **Selenium**, **Cucumber**, and **Java**, we need to set up a project with:

- Required libraries (e.g., Selenium, Cucumber, TestNG)
- A way to compile and run tests
- A structure to manage dependencies and versions
- Integration with CI/CD tools

Doing all this manually is time-consuming and error-prone. That’s where **build tools** like **Gradle** and **Maven** come in.


##  What Are Gradle and Maven?

Both are **build automation tools** that help manage:

- 📦 Dependencies (external libraries)
- 🏗️ Project builds (compile, test, package)
- 🔁 Test execution
- 📊 Reporting and plugins


## 🧩 Maven vs Gradle Comparison

| Feature            | Maven                              | Gradle                             |
|--------------------|-------------------------------------|-------------------------------------|
| Build Script       | XML (`pom.xml`)                     | Groovy/Kotlin DSL (`build.gradle`)  |
| Performance        | Slower (XML parsing)                | Faster (incremental builds, caching)|
| Flexibility        | Convention over configuration       | Highly customizable                 |
| Learning Curve     | Easier for beginners                | More flexible but steeper learning  |
| IDE Support        | Excellent                           | Excellent                           |

## how dependencies are imported in Maven and Gradle
###  Maven Example (`pom.xml`)
```xml
<dependencies>
    <dependency>
        <groupId>org.seleniumhq.selenium</groupId>
        <artifactId>selenium-java</artifactId>
        <version>4.12.1</version>
    </dependency>
    <dependency>
        <groupId>io.cucumber</groupId>
        <artifactId>cucumber-java</artifactId>
        <version>7.14.0</version>
    </dependency>
</dependencies>
```
- Maven downloads these from its central repository.
- You run: mvn clean install or mvn test
### Gradle: Using build.gradle
```
dependencies {
    testImplementation 'org.seleniumhq.selenium:selenium-java:4.12.1'
    testImplementation 'io.cucumber:cucumber-java:7.14.0'
}

```
- Gradle also pulls from Maven Central or other repositories.
- You run: gradle build or gradle test


### ✅ Why Use Gradle or Maven?
- Automatically download and manage dependencies
- Run tests with a single command (gradle test or mvn test)
- Easily integrate with CI tools like Jenkins or GitHub Actions
- Generate reports and manage plugins
- Keep your project clean, organized, and scalable

---
--- 

#  Assertions in Automation Testing

Assertions are used to validate expected outcomes in test cases. They help determine whether a test has passed or failed.

##  Hard Assert vs Soft Assert

| Feature        | Hard Assert                          | Soft Assert                          |
|----------------|--------------------------------------|--------------------------------------|
| Behavior       | Stops execution on failure           | Continues execution despite failure  |
| Use Case       | Critical validations                 | Multiple validations in one test     |
| Result         | Immediate test failure               | Collects all failures, reports at end |
| Library        | `org.testng.Assert`                  | `org.testng.asserts.SoftAssert`      |



###  Hard Assert Example (TestNG)
```java
import org.testng.Assert;

@Test
public void testLogin() {
    Assert.assertEquals(getTitle(), "Dashboard"); // If this fails, test stops here
    Assert.assertTrue(isUserLoggedIn());          // Will not execute if above fails
}
- Types of Assertions in TestNG
    - assertEquals
    - assertTrue
    - assertFalse
    - assertNotEquals
    - assertNull
    - assertNotNull
    - assertSame 
    - assertNotSame 
## 🧪 Types of Assertions in TestNG

1. **assertEquals(actual, expected)**  
   Verifies that two values are equal.
   ```java
   Assert.assertEquals(getStatusCode(), 200);
   ```

2. **assertTrue(condition)**  
   Verifies that a condition is true.
   ```java
   Assert.assertTrue(isElementVisible());
   ```

3. **assertFalse(condition)**  
   Verifies that a condition is false.
   ```java
   Assert.assertFalse(isErrorDisplayed());
   ```

4. **assertNotEquals(actual, expected)**  
   Verifies that two values are not equal.
   ```java
   Assert.assertNotEquals(getUserRole(), "Admin");
   ```

5. **assertNull(object)**  
   Verifies that an object is null.
   ```java
   Assert.assertNull(getDeletedUser());
   ```

6. **assertNotNull(object)**  
   Verifies that an object is not null.
   ```java
   Assert.assertNotNull(getActiveSession());
   ```

7. **assertSame(actual, expected)**  
   Verifies that two references point to the same object.
   ```java
   Assert.assertSame(obj1, obj2);
   ```

8. **assertNotSame(actual, expected)**  
   Verifies that two references do not point to the same object.
   ```java
   Assert.assertNotSame(obj1, obj3);
   ```

### Soft Asserts
```java
import org.testng.asserts.SoftAssert;

@Test
public void testProfile() {
    SoftAssert softAssert = new SoftAssert();
    softAssert.assertEquals(getUserName(), "Sumit");
    softAssert.assertTrue(isProfilePictureVisible());
    softAssert.assertAll(); // Reports all failures at once
}
```
- ✅ If all assertions pass → assertAll() does nothing, test passes.
- ❌ If any assertion fails → assertAll() throws an error, test fails here, not earlier.

| Class / Interface     | Description |
|-----------------------|-------------|
| `WebDriver`           | Core Selenium interface to interact with browsers. |
---
---
##  How to Take Screenshot using Selenium in Java

```java
---
public class BasePageObject {
    private Driver driver;

    protected Driver getDriver() {
        return this.driver;
    }
}
---

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;

public class Driver {
    private WebDriver webDriver;

    public Driver(WebDriver webDriver) {
        this.webDriver = webDriver;
    }

    public WebDriver getWebDriver() {
        return this.webDriver;
    }

    public void takeScreenshot(String name) {
        try {
            File src = ((TakesScreenshot) webDriver).getScreenshotAs(OutputType.FILE);
            String filePath = "./screenshots/" + name + ".png";
            FileUtils.copyFile(src, new File(filePath));
            System.out.println("Screenshot saved at: " + filePath);
        } catch (IOException e) {
            System.err.println("Snapshot could not be saved.");
            e.printStackTrace();
        }
    }
}
---
# How to call takeScreenshot method
public void takeScreenshot() {
        this.getDriver().takeScreenshot("login_success_screen"); # for ex. login successfull screen or failed screen
}
```


| Class / Interface            | Description |
|------------------------------|-------------|
| `TakesScreenshot`            | Selenium interface to take screenshots. |
| `File` (Java IO)      | Represents file/directory paths for reading/writing. |
| `IOException`         | Handles input/output exceptions, such as file save errors. |
| `OutputType`                 | Enum to define output format (e.g., `FILE`). |
| `FileUtils` (Apache Commons) | Utility class to copy/move files easily. |

##  Maven Dependency for Apache Commons IO

Make sure to include this in your `pom.xml`:

```xml
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.11.0</version>
</dependency>
```
### 🔧 How It Works:
- Casts `WebDriver` to `TakesScreenshot` to enable screenshot capability.
- Captures the screenshot using `getScreenshotAs(OutputType.FILE)`.
- Saves the screenshot to a local folder using `FileUtils.copyFile()`.


- Ensure `./screenshots/` directory exists or create it before running tests.

---
---

