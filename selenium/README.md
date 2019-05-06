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
