# qaf-step-by-step-tutorial
qaf getting started tutorial provides step by step exercise to start using [QAF](https://qmetry.github.io/qaf).

##### TOC

 - [Exercise-1](#exercise-1)
   - [Pre-requisites](#pre-requisites)
     - [QAS users](#qas-users)
     - [Eclipse Users](#eclipse-users)
   - [Create New Project](#create-new-project)
 - [Exercise-2](#exercise-2)
   - [Create locator repository](#create-locator-repository)
   - [Create your first Test case in BDD](#create-your-first-test-case-in-bdd)
   - [Create your first Test case in Java](#create-your-first-test-case-in-java)
   - [References](#references)

_____

# Exercise-1

This is the first step to start automation using QAF.


## Pre-requisites

Required java 1.7 or later, you can obtain it from [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

### QAS users

Create new automation project.

### Eclipse Users

 1. Setup your local environment, if don't have Eclipse IDE, [Download and install the Eclipse IDE](https://eclipse.org/downloads/).
 2. Following plugins are recommanded for eclipse users. 
   * [TestNG](http://testng.org/doc/eclipse.html)
   * [Apache IvyDE plugin](https://ant.apache.org/ivy/ivyde/download.html)
   * [BDD Editor plugin](https://qmetry.github.io/qaf/editor/bdd/eclipse/) - BDD and Gherkin Editor for BDD test authoring

## Create New Project

   Download [qaf-example-project-skeleton.zip](https://github.com/qmetry/qaf-step-by-step-tutorial/releases/download/Exercise-1/qaf-example-project-skeleton.zip). You can directly import project in Eclipse, refer [Importing existing projects](http://help.eclipse.org/kepler/topic/org.eclipse.platform.doc.user/tasks/tasks-importproject.htm?cp=0_3_10_0) for help. Example project uses ANT as build tool and IVY for dependncy management.

# Exercise-2

____

After completion of [Exercise-1](https://github.com/qmetry/qaf-step-by-step-tutorial/tree/Exercise-1) you will have your local enviroment ready with project skeleton in eclipse. Now you are ready to create your first automated test. 

In this exercise we will create sample test case to automate google serach.
Conisder following test case:
```
Open Google search page
Search for Git reporsitory QMetry Automation Framework
Verify that Git repository link present 
```
## Create locator repository
To start with first of all you need to identify element locators and place into locator repositoiry.
QAS user can use object-spy featuer and non QAS users can use firebug with firepath.

Create new locator repository named `home.properties` and provide locators for serach box, and search button. 
``` properties
txt.searchbox = name=q
btn.search = name=btnG
```

## Create your first Test case in BDD

 1. Create new BDD file named `suite-1.bdd` in scenarios dir
 2. Open this file in BDD editor
 3. Create new Scenario with name 'SampleTest', Description 'Sample Test Scenario' and group 'SMOKE'.
    * if you are using QAS create new scenario following new scenario wizard
    * if you are using eclipse with QAF bdd editor press ctrl+space and select Scenario snnipet
 4. You will have scenario skeleton ready as below:
   ``` javascript
    SCENARIO: SampleTest
    META-DATA: {"description":"Sample Test Scenario","groups":["SMOKE"]}

    END
   ```
 5. Call teststeps in your Scenario. To start with for this example of google you can call predefined steps avialable with QAF-Support jar (Make sure that ivy has QAF-Support dependency added). Call steps as bellow 
 
    ``` javascript
    SCENARIO: SampleTest
    META-DATA: {"description":"Sample Test Scenario","groups":["SMOKE"]}
	    Given get '/'
	    When sendkeys 'Git reporsitory QAF' to 'txt.searchbox'
	    And click on 'btn.search'
	    Then verify link with partial text 'qaf' is present 
    END
    ```

## Create your first Test case in Java 

 1. Create new Java Class `Suite1.java` extending 'com.qmetry.qaf.automation.ui.WebDriverTestCase' under package `qaf.example.tests` in src dir. Refer [Creating a Java class](http://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-9.htm) for help. Your class should look like:
 
 ``` java
package qaf.example.tests;

import org.testng.annotations.Test;
import com.qmetry.qaf.automation.ui.WebDriverTestCase;

public class Suite1 extends WebDriverTestCase {

}
 ```
 2. create new test method `SampleTest`, add import statement `import org.testng.annotations.Test;`, provide `@Test` annotation, set decription and groups
 
 ```java
 	@Test(description="Sample Test Scenario", groups={"SMOKE"})
	public void testGoogleSearch() {
	
	}
 ```
 
 3. add import statement `import static com.qmetry.qaf.automation.step.CommonStep.*;`. Use content assist (ctrl + SPACE) to refer available methods. Call steps in test method as bellow:
 
 ```java
 	   get("/");
	   sendKeys("Git reporsitory QAF", "txt.searchbox");
	   click("btn.search");
	   verifyLinkWithPartialTextPresent("qaf");
 ```
 
 your complete class with testcase will look like
 
 ``` Java
package qaf.example.tests;

import org.testng.annotations.Test;
import com.qmetry.qaf.automation.ui.WebDriverTestCase;

public class Suite1 extends WebDriverTestCase {

	@Test(description="Sample Test Scenario", groups={"SMOKE"})
	public void testGoogleSearch() {
	   get("/");
	   sendKeys("Git reporsitory QAF", "txt.searchbox");
	   click("btn.search");
	   verifyLinkWithPartialTextPresent("qaf");
	}
}
 ```

### References
 1. <a href="https://qmetry.github.io/qaf/latest/understand_dirstructure.html" target="_blank">Understating Directory Structure:link:</a>
 2. <a href="https://qmetry.github.io/qaf/latest/locator_repository.html" target="_blank">Locator Repository:link:</a>
 3. <a href="https://qmetry.github.io/qaf/latest/scenario.html" target="_blank">Test Authoring in BDD:link:</a>

