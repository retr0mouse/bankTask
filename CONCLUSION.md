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
- The checks in the setState function of the _submitForm in the LoanForm are somewhat redundant. The tempAmount and tempPeriod variables are parsed from the result map and then used in a conditional statement. However, regardless of the condition's outcome, the _loanAmountResult and _loanPeriodResult variables are set to the same values (tempAmount and tempPeriod respectively, or _loanAmount and _loanPeriod). (fixed)
- The LoanForm widget could benefit from more abstraction. For instance, the sliders for the loan amount and period could be extracted into their own widgets. (fixed)
- It would be helpful to describe what each test is doing in the api_service_test file, currently there are no comments explaining the behaviour. (fixed)
- In the LoanPeriod slider the lowest value that you can have is 6 months, while the text says '12 months'. (fixed)
- LoanPeriod slider divisions are not correct should be `48` instead of `40`. (fixed)
- `inbank-frontend-98f09aabec29a741365f750db29dfe606f20f0b2` folder should be removed from the repository, I believe it was added by accident. (fixed)
- Bonus: in the LoanForm widget, when we get an error, we could benefit from hiding the results texts, because currently it is too cluttered. (fixed)

## Backend
- The DecisionEngine class seems to have multiple responsibilities (validating the personal ID code, calculating the credit modifier, and calculating the loan amount and period). This violates the Single Responsibility Principle (SRP) of SOLID. It would be better to separate these responsibilities into different classes if we plan to add additional checks or to test the application more thoroughly.
- Decision engine does not return the maximum possible loan sum, instead it calculates the sum that is equal or less than requested.

## Most Important Shortcomings of TICKET-101:
- Too many requests from the frontend to the backend. Whenever the values of sliders change, we check if the loan is approved with these values. A better approach would be to have an onReleased() to fire the request or even to add a button to submit the values. (fixed)
- The implementation of the decision engine on the backend was not implemented correctly, meaning it does not use credit score to decide whether we can approve the request for loan or not. (fixed)
### Solution:
- Implemented a solution for making much less request from the frontend to the backend. Created a button to send requests, refactored tests accordingly.
- Refactored the decision engine to use credit score to determine the validity of the loan request. 

# TICKET-102 Implementation Plan
For TICKET-102, which involves implementing additional functionality for the decision engine, which takes into account customer's age, I propose following plan:

## Requirements:
- Implementation should not introduce new input fields
- Decision engine should work
- When the returned decision is negative because of the age of customer, it is clearly pointed out by the error that shows on screen

## Implementation Steps:
1. **Analysis and Design**: I evaluate the current implementation of the decision engine and exceptions to add the functionality in compliance with everything
2. **Implementation**: Add a function to get the age of the user, add exception to throw when the age is not approved and the condition in which this error will be thrown
3. **Testing**: Write additional tests to check the correctness of the added functionality 
