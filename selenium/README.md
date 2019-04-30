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
