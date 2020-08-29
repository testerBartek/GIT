# Selenium WebDriver

## Tests on Browsers

Remember to check version of WebDriver with current browser version.

1. Create a new Python Package in your project
2. Create a new Python File \(and then code and run there\)

### Mozilla Firefox

Firefox WebDriver is called geckodriver.exe

{% embed url="https://www.selenium.dev/selenium/docs/api/javascript/module/selenium-webdriver/firefox.html" caption="page information\'s " %}

{% embed url="https://github.com/mozilla/geckodriver/releases/" caption="geckodriver" %}

```python
from selenium import webdriver

class RunFFTests():
    def testMethod(self):
        driver = webdriver.Firefox(executable_path="C:\\Users\\nn\\PycharmProjects\\drivers\\geckodriver.exe")
        driver.get("http://www.google.com")

ff = RunFFTests()
ff.testMethod()

```

After this program the Firefox doesn't close.

#### Xpath

{% embed url="https://letskodeit.teachable.com/p/practice" caption="website to practice" %}

![Add-ons Try](.gitbook/assets/image%20%2868%29.png)

![Xpath in firefox console](.gitbook/assets/image%20%2823%29.png)

```python
#examples
$x("//input[@id='input']")
$x("//input[contains(@class, 'btn-style')]")
$x("//input[@class='btn-style']")
```



### Google Chrome

Google Chrome driver is call chromedriver.exe

{% embed url="https://chromedriver.chromium.org/" %}

```python
from selenium import webdriver

# class ChromeDriver():
#     def testMethod(self):
#         driver = webdriver.Chrome(executable_path="C:\\Users\\nn\\PycharmProjects\\drivers\\chromedriver.exe")
#         driver.get("http://www.google.com")
#
# cc = ChromeDriver()
# cc.testMethod()

driver = webdriver.Chrome(executable_path="C:\\Users\\nn\\PycharmProjects\\drivers\\chromedriver.exe")
driver.get("http://www.google.com")
```

When using class in ChromeDriver, after the page is load the browser will close. Without class the browser stay on this site.

#### Xpath

![Find elements by use cltr+F](.gitbook/assets/image%20%2859%29.png)

![In Console](.gitbook/assets/image%20%288%29.png)

Extension **Ranorex Selocity**

1. Inspect element
2. Ranorex Selocity show &lt;input&gt; css / xpath to copy to automation tests

![Ranorex Selocity how to use ](.gitbook/assets/image%20%2815%29.png)

### Internet Explorer

Internet Explorer driver is called IEDriverServer.exe

{% embed url="https://www.selenium.dev/downloads/" %}

#### Requirements to run tests on Internet Explorer

1. Set a zoom on 100%

![](.gitbook/assets/image%20%2860%29.png)

2. Make sure that Protected Mode on every of 4 types of zone are the same \(Disable or Enable\)  
a\) Internet  
b\) Local intranet  
c\) Trusted sites  
d\) Restricted sites

![](.gitbook/assets/image%20%2824%29.png)

```python
from selenium import webdriver

class IEDriverWindows():
    def testMethod(self):
        driver = webdriver.Ie(executable_path="C:\\Users\\nn\\PycharmProjects\\drivers\\IEDriverServer.exe")
        driver.get("http://www.google.com")

ieObject = IEDriverWindows()
ieObject.testMethod()

```

### Safari

It's only supported on Macs. \(Apple\)

## Commands

### import webdriver

```python
from selenium import webdriver #use a selenium package
```

### set a webdriver

```python
#chrome
driver = webdriver.Chrome(executable_path="C:\\Users\\nn\\PycharmProjects\\drivers\\chromedriver.exe")
#firefox
driver = webdriver.Firefox(executable_path="C:\\Users\\nn\\PycharmProjects\\drivers\\geckodriver.exe")
#IE
driver = webdriver.Ie(executable_path="C:\\Users\\nn\\PycharmProjects\\drivers\\IEDriverServer.exe")
```

### open a URL

```python
#e.g. www.google.com
driver.get("http://www.google.com")
```

## Finding elements



### By

```python
#to use 'By' need to import lib
from selenium.webdriver.common.by import By
```

```python
class By(object):
    """
    Set of supported locator strategies.
    """

    ID = "id"
    XPATH = "xpath"
    LINK_TEXT = "link text"
    PARTIAL_LINK_TEXT = "partial link text"
    NAME = "name"
    TAG_NAME = "tag name"
    CLASS_NAME = "class name"
    CSS_SELECTOR = "css selector"
```

```python
driver.find_element(By.XPATH,	"xpath	expression")
#e.g.
elementById = driver.find_element(By.ID, "name")
driver.find_element(By.XPATH, "//input[@id='displayed-text']")
elementByClassName = driver.find_element(By.CLASS_NAME, "table-display")
```

