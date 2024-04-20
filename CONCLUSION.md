# TICKET-101 Validation Conclusion

## Overview
In this conclusion, I evaluate the implementation of TICKET-101, which aimed to implement the MVP scope of the decision engine.

### What was done well:
- The intern successfully created the loan form in Flutter framework on the backend and the decision engine in Spring Boot on the backend.
- The code works according to the requirements.

## Frontend
- The implementation is well-documented, it is easy to understand what the code does only by reading the comments and names of the functions and parameters.
- Key components are split into separate files and classes (test files as well), which helps to better understand how the program behaves, maintain it easier.
- The use of `const` constructors where possible is good for performance and memory usage, especially for widgets that are build frequently. Because when you use const to create an instance of a class, Dart ensures that only a single instance of that object exists in memory and reuses it each time it encounters a const constructor with the same parameters.
- The use of theme data for consistent styling across the app is a good practice. 
- The tests cover the main functionalities of the LoanForm widget, such as displaying the form and initial values, and changing the load amount and period with the sliders.

## Backend
- The code is DRY (Don't Repeat Yourself!), meaning the code seems to avoid unnecessary repetition.
- The code is well-structured and follows the MVC pattern, which makes it easy to understand and maintain.
- The use of custom exceptions for different error scenarios is a good practice. It makes error handling more precise and informative.
- The use of data transfer objects (DTOs) for request and response data is a good practice. It decouples the API layer from the service layer and makes the code more flexible.

### Areas for Improvement:

## Frontend
- The checks in the setState function of the _submitForm in the LoanForm are somewhat redundant. The tempAmount and tempPeriod variables are parsed from the result map and then used in a conditional statement. However, regardless of the condition's outcome, the _loanAmountResult and _loanPeriodResult variables are set to the same values (tempAmount and tempPeriod respectively, or _loanAmount and _loanPeriod).
- The LoanForm widget could benefit from more abstraction. For instance, the sliders for the loan amount and period could be extracted into their own widgets.
- It would be helpful to describe what each test is doing in the api_service_test file, currently there are no comments explaining the behaviour.
- In the LoanPeriod slider the lowest value that you can have is 6 months, while the text says '12 months'
- LoanPeriod slider divisions are not correct should be `48` instead of `40`
- `inbank-frontend-98f09aabec29a741365f750db29dfe606f20f0b2` folder should be removed from the repository, I believe it was added by accident
- Bonus: in the LoanForm widget, when we get an error, we could benefit from hiding the results texts, because currently it is too cluttered

## Backend
- The DecisionEngine class seems to have multiple responsibilities (validating the personal ID code, calculating the credit modifier, and calculating the loan amount and period). This violates the Single Responsibility Principle (SRP) of SOLID. It would be better to separate these responsibilities into different classes.
- The DecisionEngineController directly uses the DecisionEngine service. This makes the controller tightly coupled with the service. It would be better to use dependency injection to inject the service into the controller. This would make the code more flexible and easier to test.
- Credit score calculation is implemented incorrectly. Current implementation: (credit score * loan period) ; Should be: ((credit modifier / loan amount) * loan period).

## Most Important Shortcoming of TICKET-101:
- Too many requests from the frontend to the backend. Whenever the values of sliders change, we check if the loan is approved with these values. A better approach would be to have an onReleased() to fire the request or even to add a button to submit the values. I chose the latter option and implemented it.
### Solution:

# TICKET-102 Implementation Plan
For TICKET-102, which involves implementing additional functionality for the decision engine, which takes into account customer's age, I propose following plan:

## Requirements:
- Implementation should not introduce new input fields
- Ensure that the decision engine returns the maximum approved loan amount as before
- When the returned decision is negative because of the age of customer, it is clearly pointed out by the error that shows on screen

## Implementation Steps:
1. **Analysis and Design**: I evaluate the current implementation of the decision engine and exceptions to add the functionality in compliance with everything
2. **Implementation**: Add a function to get the age of the user, add exception to throw when the age is not approved and the condition in which this error will be thrown
3. **Testing**: Write additional tests to check the correctness of the added functionality 
