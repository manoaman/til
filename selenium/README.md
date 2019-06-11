### How to click on a pull down menu which uses span and a tags?

```
 List<WebElement> element = driver.findElements(By.cssSelector(".txt_black.heading_4"));
    for (int i = 0; i < element.size(); i++) {
        String temp = element.get(i).getText();
        if (temp.equals("0")) {
            element.get(i).click();             
            break;
        }
    }
```

https://stackoverflow.com/questions/26689428/how-to-select-the-value-from-span-type-dropdown-in-selenium-webdriver

### How to setup chromedriver to do headless Selenium tests to work in conjunction with Docker container?

```
                // Add these to test if Selenium works on Linux
                ChromeOptions options = new ChromeOptions();
                options.addArguments("--no-sandbox");
                options.addArguments("--headless");
                options.addArguments("--disable-dev-shm-usage");

                DesiredCapabilities capabilities = DesiredCapabilities.chrome();
                capabilities.setCapability(ChromeOptions.CAPABILITY, options);
```

https://github.com/heroku/heroku-buildpack-google-chrome/issues/46
https://stackoverflow.com/questions/23834413/pass-driver-chromeoptions-and-desiredcapabilities
https://stackoverflow.com/questions/50642308/webdriverexception-unknown-error-devtoolsactiveport-file-doesnt-exist-while-t

### How to use Explicit Waits?

```
WebDriver driver = new FirefoxDriver();
driver.get("http://somedomain/url_that_delays_loading");
WebElement myDynamicElement = (new WebDriverWait(driver, 10))
  .until(ExpectedConditions.presenceOfElementLocated(By.id("myDynamicElement")));
```
https://docs.seleniumhq.org/docs/04_webdriver_advanced.jsp


### Why am I receiving "Selenium Error: no display specified"?

`DISPLAY` variable needs to be set to run a headless chromedriver.  With DISPLAY=localhost:0.0 you are asking to connect to an X11 server via TCP. Your X server is most likely not listening on a TCP socket.

```
export DISPLAY=localhost:0.0
```
https://stackoverflow.com/questions/24653127/selenium-error-no-display-specified
https://www.linuxquestions.org/questions/linux-newbie-8/display%3D-0-0-vs-display%3Dlocalhost-0-0-a-933940/

Note:  What is Xvbf?

```
Xvfb is a virtual display framebuffer for X - the display system used by Linux. It provides a fake display buffer for graphical programs to write to, thus allowing any program to run headlessly.Jan 9, 2015
```
http://tobyho.com/2015/01/09/headless-browser-testing-xvfb/


#### What is the workaround when an element is not clickable?

Use JavaScript executor to directly click on an element.

```
WebElement ele = driver.findElement(By.xpath("element_xpath"));
JavascriptExecutor executor = (JavascriptExecutor)driver;
executor.executeScript("arguments[0].click();", ele);
```
https://stackoverflow.com/questions/44912203/selenium-web-driver-java-element-is-not-clickable-at-point-x-y-other-elem
