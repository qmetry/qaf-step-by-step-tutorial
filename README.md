# qaf-step-by-step-tutorial
qaf getting started tutorial provide step by step exercise 

This repository provides a step by step guide to start using QAF.

#Exercise-2

After completion of [Exercise-1](../tree/Exercise-1) you will have your local enviroment ready with project skeleton in eclipse. Now you are ready to create your first automated test. 

In this exercise we will create sample test case to automate google serach.
Conisder following test case:
```
Open Google search page
Search for Git reporsitory QMetry Automation Framework
Verify that Git repository link present 
```

### Create locator repository
To start with first of all you need to identify element locators and place into locator repositoiry.
QAS user can use object-spy featuer and non QAS users can use firebug with firepath.

Create new locator repository named `home.properties` and provide locators for serach box, and search button. 
``` properties
txt.searchbox = name=q
btn.search = name=btnG
```

### Create your first Test case
1. Create new BDD file named `suite-1.bdd` in scenarios dir
2. Open this file in BDD editor
3. Create new Scenario with name 'SampleTest', Description 'Sample Test Scenario' and group 'SMOKE'.
    * if you are using QAS create new scenario following new scenario wizard
    * if you are using eclipse with QAF bdd editor press ctrl+space and select Scenario snnipet
4. You will have scenario skeleton ready as below:
   ``` bdd
    SCENARIO: SampleTest
    META-DATA: {"description":"Sample Test Scenario","groups":["SMOKE"]}

    END
   ```
5. Call teststeps in your Scenario. To start with for this example of google you can call predefined steps avialable with QAF-Support jar (Make sure that ivy has QAF-Support dependency added). Call steps as bellow 
 
    ``` bdd
    SCENARIO: SampleTest
    META-DATA: {"description":"Sample Test Scenario","groups":["SMOKE"]}
      Given get '/'
	    When sendkeys 'Git reporsitory QAF' to 'txt.searchbox'
	    And click on 'btn.search'
	    Then verify 'link=QMetry Automation Framework' present 
    END
    ```
