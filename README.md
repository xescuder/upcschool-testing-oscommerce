This is a practical case for UPC School postgraduates, where:

- Selenium tests are created
- We add reporting of results
- We do exploratory testing with Capture for JIRA


## Test reporting

Test reporting is done with Allure.

1. Execute tests with ```verify``` goal of maven
1. From terminal execute ```mvn allure:serve```

### Step 2: Add description to tests

Use annotation `Description`

```java
@Test
@Description("Testing Samsung models")
void test1() {
    process.enterSite(OSCOMMERCE_URL);
    process.selectProduct("Samsung");
    process.addToCart();
    process.updateQuantity("2");
    process.signInProcess();
    process.processOrderAndConfirm();
}
```

### Step 3: Add steps


```
@Step("Selecting product {product}")
public void selectProduct(String product) {
    if(product.equals("Samsung")) {
        catalog.clickSamsungGalaxyTab(wait);
    }
    if (product.equals("Beloved")) {
        catalog.clickBeloved(wait);
    }
}
```

#### Step 4: Add severity

```
@Severity(SeverityLevel.CRITICAL)
void test1() {
```


#### Step 5: Adding screenshots

```java
package upcschool.oscommerce.test;

import io.qameta.allure.Attachment;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;

public class ScreenshotUtils {
    @Attachment(type = "image/png")
    public static byte[] screenshot(WebDriver driver)/* throws IOException */ {
        return ((TakesScreenshot) driver).getScreenshotAs(OutputType.BYTES);
    }
}
```

Now call it from test if you want to screenshot.

```java
void test1() {
    ScreenshotUtils.screenshot(driver);
```

### Step 6: Add failing assertion

Add a failed assertion and check how report changes.

```
Assertions.assertEquals(false,true);
```



