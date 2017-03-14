---
layout: default   
permalink: /Feature Demos/Live Unit Testing/     
---

# Live Unit Testing

## Overview 
Live Unit Testing is a new feature introduced in Visual Studio 2017. This feature visualizes unit test results and code coverage live on the editor, while you are coding. It works with C\#/VB projects for .NET framework and supports three test frameworks of MSTest, xUnit and NUnit.

This feature makes it easy to maintain quality and test coverage during rapid development and take your productivity to a whole new level. Imagine fixing a bug in a code base which you may not be completely familiar with. With Live Unit Testing you can know right away -as you are making edits to fix the bug - that you did not break any other part of the system. Getting this feedback, in-situ, as you type will give you extra confidence, make you more productive and why not, even enjoying fixing bugs and writing unit tests!

<img src="./images/VisualStudioTools.png">

Live Unit Testing automatically runs the impacted unit tests in the background as you edit code, and visualizes the results and code coverage live, in the editor, in real-time. In addition to giving feedback on the impact that your changes had on the existing tests, you also get immediate feedback on whether the new code you added is already covered by one or more existing tests. This will gently remind you to write unit tests as you are making bug fixes or adding features. With Live Unit Testing you're on your way to removing the test debt in your code base!

## Related News
[Live Unit Testing on MSDN blog](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/live-unit-testing-visual-studio-2017-rc/)

## Prerequisites
- If you prefer to use your own machine, you will need:    
   - Visual Studio 2017 (download [here](https://www.visualstudio.com/vs/visual-studio-2017-rc/))
   - Download the Parts Unlimited project [here](https://github.com/Microsoft/PartsUnlimited/tree/aspnet45)

- If you prefer to use download the demo vm pre-installed with 2017 RC and fully configured, please see the instructions [here](../../demovm/)
    

## Setup    
 - Checkout the LiveUnitTesting branch to get started
    From a command or Powershell prompt, browse to the code repo and type:
    `git checkout LiveUnitTesting`
 - (Alternative Path) Instead of using the git branch you can remove the ToLower() method call in LINQ query in the Search() method found in StringContainsProductSearch.cs file.
 - Open PartsUnlimited.sln in Visual Studio 2017
 - Rebuild the solution (Ctrl-Shift-B)


## Demo Steps
> **Talking Point**: <br />
 Let us start with the introduction of Live Unit Testing - Live Unit Testing is a new feature introduced in Visual Studio 2017 and is and it’s available for C# and VB projects that target the .NET Framework. It uses VB and C# compilers to instrument the code at compile time. Next, it runs unit tests on the instrumented code to generate data which it analyzes to understand which tests are covering which lines of code. It then uses this data to run just those tests that were impacted by the given edit providing immediate feedback on the results in the editor itself. As more edits are made or more tests are added or removed, it continuously updates the data which is used to identify the impacted tests. <br /><br />Here I am going to use the Parts Unlimited - an ASP.NET based e-commerce application for the demo.

1. Ensure *PartsUnlimited.sln* is open in Visual Studio 
    
    <img src="./images/image1.png"  />

1. In Solution Explorer, navigate to project **PartsUnlimitedWebsite** and open file ***StringContainsProductSearch.cs***

1. Walk thru the code at a high-level to help audience understand the logic 

> **Talking Point**: <br />Let's look at this method that I am working on called ***Search*** that returns products that has the names matching the LINQ query<br /><br /> I have written some unit tests for this ***Search*** method already, and instead of Doing a “Run All Tests” to see what is passing, I am going to start Live Unit Testing.

1. Click ***Tests -> Live Unit Testing -> Start***
    <img src="./images/image2.png"  />

1. Wait till the unit test coverage glyphs appear.
    <img src="./images/image3.png"  />

> **Talking Point**: <br />I can see Red Xs, Green Checks and Blue Dashes. Each of these glyphs tells me my test coverage and if any tests touching that line are failing - Blue Dashes indicate no unit test coverage - Red Xs indicate unit test code is failing - Green checks indicate unit test code is passing.<br /><br />Looks like I have a lot of failing tests!

1. Click on an X and then scroll down to click on a Check 

> **Talking Point**: <br />When I click on an X or a check, I can see which tests specifically are passing or failing. I can select a test to navigate to my test method.

1. Open ***StringContainsProductSearch.cs*** and ***ProductSearchTests.cs*** side-by-side.

> **Talking Point**: <br />Let's say we are trying to modify the Search method. As you can see there are tests failing on this method. We need to resolve those first - "you touch it, you test it!"

1. Make the following edit in the method to add ToLower() to the change the product title to lower case 
    ````C#
    var q = _context.Products
              .Where(p => p.Title.ToLower().Contains(cleanQuery));
    ````
    <img src="./images/image6.png" />   

1. After you make the code change, wait for a couple of seconds and show how ***Search()*** is passing the unit test now and the coverage glyph turns from Red X to Green check. 
Point out how it was all live and you did not have to manually go and run the unit test.
    <img src="./images/image7.png" />

> **Talking Point**: <br />As you can see, the tests are all now passing. And we've done the right thing by leaving the code in a better state than when we found it.

-------
### Conclusion 
 Live Unit Testing will improve your developer productivity, test coverage and quality of software. .NET developers out there, please do check out this feature in Visual Studio 2017. For developers who are part of a team that practices test-driven development, Live Unit Testing gamifies their workflow; in other words, all their tests will be failing at first, and as they implement each method they will see them turn green. It will evoke the same feeling as a nod of approval from your coach, who is watching you intently from the sidelines, as you practice your art!







