# MteSenseWdd
This is tiny test automation tool for dynamic debug with webdriver incude Selenium, Appium. And you can use this as library for your test automation project with webdriver in any java ide, it's very easy to deploy and use. Now support many webdriver type include chrome, firefox, safari, ios, and android.
# Release History
- MteSenseWdd beta 0.1.1 : support Selenium and Appium with webdriver. 
# Requirements
You need add these jars as libraries in your project to use MteSenseWdd function.
- selenium standalone jar
- appium java client
- junit(optional) 
# Installation
- add MteSense-Wdd-beta-0.1.1.jar into your test automation project.
# How to use
#### Step 1 :
Add MteSense-Wdd-beta-0.1.1.jar into your project classpath.
#### Step 2 :
Create java file to build webdriver, please pay attention to your driver type like below:

```java
package com.mte.wdd.test;

import com.mte.wdd.main.MteSenseLoader;
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.remote.CapabilityType;
import org.openqa.selenium.remote.DesiredCapabilities;

import java.util.concurrent.TimeUnit;

/**
 * Created by java on 20/07/2017.
 */
public class MteSenseWdadTest {

    ChromeDriver driver;

    @Before
    public void setUp() throws Exception {
        System.setProperty("webdriver.chrome.driver", "./config/chromedriver");
        DesiredCapabilities capabilities = DesiredCapabilities.chrome();
        capabilities.setCapability(CapabilityType.ACCEPT_SSL_CERTS, true);
        driver = new ChromeDriver(capabilities);

        driver.manage().timeouts()
                .pageLoadTimeout(20, TimeUnit.SECONDS);

        driver.manage().timeouts()
                .implicitlyWait(10, TimeUnit.SECONDS);

        driver.manage().timeouts()
                .setScriptTimeout(10, TimeUnit.SECONDS);
        driver.manage().window().maximize();
    }

    @Test
    public void testMain() throws Exception {

        MteSenseLoader loader = new MteSenseLoader();

        loader.senseLoader("chrome","./src/MteSenseInstanceUpdate.java", "MteSenseInstanceUpdate", "http://www.baidu.com", "runDynamicAction", driver);

    }

    @After
    public void tearDown() throws Exception {
        driver.quit();
    }

}

```
#### MteSenseInstanceUpdate
```java
import org.openqa.selenium.chrome.ChromeDriver;

/**
 * Created by java on 20/07/2017.
 */
public class MteSenseInstanceUpdate {

    public static void runDynamicAction(ChromeDriver driver) {

        driver.findElementById("kw").sendKeys("Testerhome");
        driver.findElementById("su").click();
//        driver.get("http://wwww.baidu.com");

    }

}

```

#### Please pay attention to following code:

```java
        MteSenseLoader loader = new MteSenseLoader();
        loader.senseLoader("chrome","./src/MteSenseInstanceUpdate.java", "MteSenseInstanceUpdate", "http://www.baidu.com", "runDynamicAction", driver);
```
There are 6 parameters for this method as below:
- driver type : the driver type should be same with what you have created in your script.
- full file path : this file shoud be target file what you need create for modifying. That means you will update this file to debug with webdriver.
- full class name : this class name should be same with your target java file for modifying. If this java file hasn't package name, you can input class name, otherwise you need input package name+class name like com.xxx.xxx.xxx.MteSenseInstanceUpdate.
- tartget url : sometime you can keep this parameter as null, because when you debug mobile webdriver like iosdriver or androiddriver, you don't need url.
- target method name in your target java file for modifying, most of time you need debug operation in this method
- your webriver instance what you have created

# Declaration
In this project, some source codes come from internet and other test automation project, the purpose is only for sharing and communication with everyone who like test automation. If you don't want to integrate your code, please tell me to remove them. Thanks
