# MteSenseWdd
This is tiny test automation tool for dynamic debug with webdriver incude Selenium, Appium. And you can use this as library for your test automation project with webdriver by any java ide, it's very easy to deploy and use. Now support some webdriver types include chrome, firefox, safari, ios, and android.
# Release History
### MteSenseWdd beta 0.2.2
- Update MteSenseLoader to support non static method.

```java
// Ok
public void runDynamicAction(ChromeDriver driver) {
.........
}
// Ok
public static void runDynamicAction(ChromeDriver driver) {
.........
}

```
### MteSenseWdd beta 0.2.1
- handle url as blank.

### MteSenseWdd beta 0.2.0
- add new method to build senseLoader() function.

```java
        MteSenseLoader loader = new MteSenseLoader();

        MteSenseLoaderOptions options=new MteSenseLoaderOptions();

        options.setLoaderOption("mtesensewdd.webDriverType","chrome");
        options.setLoaderOption("mtesensewdd.fullFilePath","./src/MteSenseInstanceUpdate.java");
        options.setLoaderOption("mtesensewdd.fullClassName","MteSenseInstanceUpdate");
        options.setLoaderOption("mtesensewdd.url","http://www.baidu.com");
        options.setLoaderOption("mtesensewdd.methodName","runDynamicAction");

        loader.senseLoader(options,driver);

```
### MteSenseWdd beta 0.1.2
- update description for action codes.

### MteSenseWdd beta 0.1.1
- upport Selenium and Appium with webdriver. 

# Requirements
You need add these jars as libraries in your project to use MteSenseWdd function.
- JDK 8 or above, you need JDK to compile java code.
- selenium standalone jar
- appium java client
- junit(optional) 

# Installation
- add MteSense-Wdd-beta-x.x.x.jar into your test automation project.

# How to use
#### Step 1 :
Add MteSense-Wdd-beta-x.x.x.jar into your project classpath.

#### Step 2 :
Create java file to build webdriver, please pay attention to your driver type like below:

#### MteSenseWdadTest

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

#### There are 6 parameters for this method as below:
- driver type : the driver type should be same with what you have created in your script.
- full file path : this file shoud be target file what you need create for modifying. That means you will update this file to debug with webdriver.
- full class name : this class name should be same with your target java file for modifying. If this java file hasn't package name, you can input class name, otherwise you need input package name+class name like com.xxx.xxx.xxx.MteSenseInstanceUpdate.
- tartget url : sometime you can keep this parameter as null, because when you debug mobile webdriver like iosdriver or androiddriver, you don't need url.
- target method name in your target java file for modifying, most of time you need debug operation in this method
- your webriver instance what you have created.

#### Step 3 :
For example :
- Run MteSenseWdadTest as junit
- Change your target method code(runDynamicAction()) for your new operation and save to debug with webdriver.
- At last enjoy it ^-^.

#### Some important things

- You shoul be sure about you can start webdriver with your script.
- You only need change code in target method in your target java file for modifying.
- Every time when you update your target method like runDynamicAction() and save, the MteSenseLoader method will compile target java file to execute new operation what you have created.
- In target method, the webdriver parameter must be same to what you have created.
- Sometime you also can create java file to invoke MteSenseLoader like standalone java file to handle target java file.
- For this tool, just help you to debug your operation with webdriver include selenium and appium, you can't use debug operation to replace your real automation script.
- If you use IDEA, please uncheck with "Use "Safe Write"" item under Preferences-->Appearance&Behavior-->System Settings.

# Screencapture

![MteSenseWdd](https://github.com/PandaSense/MteSenseWdd/blob/master/image/MteSenseWddPic001.png)

# Declaration
In this project, some source codes come from internet and other test automation project, the purpose is only for sharing and communication with everyone who like test automation. If you don't want to integrate your code, please tell me to remove them. Thanks
