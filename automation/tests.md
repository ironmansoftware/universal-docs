---
description: PowerShell Universal automated test support.
---

# Tests

{% hint style="info" %}
This feature requires a [license](../licensing.md).
{% endhint %}

PowerShell Universal integrates with the [Pester ](https://pester.dev/)test framework to allow you to execute test suites and view results. Results are stored in the PowerShell Universal database so you can view historical results.

You can work with tests by visiting Automation \ Tests.

## Test Discovery

Tests files are located based on file name. Any files found in the respository that end in `.Tests.ps1` will be listed in the Test Files tab. You can create new test files on the Automation \ Scripts page.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption><p>Test Files</p></figcaption></figure>

## Test Execution

{% hint style="info" %}
Pester v5 or later needs to be installed to run tests.
{% endhint %}

Tests can be run by clicking the Run Test or Run All Tests buttons. Run Test will run the individual Test Files and Run All Tests will run all the Test Files.

You will have the option to select the environment, credential and computer to run the tests.

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Run Tests</p></figcaption></figure>

## Test Results

Test Results are produced after the test run finishes. You will be able to see the overal status of the test run and the result of individual test suites and cases.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Test Results</p></figcaption></figure>
