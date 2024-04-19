# TICKET-101 Validation Conclusion

## Overview
In this conclusion, I evaluate the implementation of TICKET-101, which aimed to implement the MVP scope of the decision engine.

### What was done well:
- The intern successfully created the loan form in Flutter framework on the backend and the decision engine in Spring Boot on the backend.

## Frontend
- The implementation is well-documented, it is easy to understand what the code does only by reading the comments and names of the functions and parameters.
- Key components are split into separate files and classes (test files as well), which helps to better understand how the program behaves, maintain it easier.
- The use of `const` constructors where possible is good for performance and memory usage, especially for widgets that are build frequently. Because when you use const to create an instance of a class, Dart ensures that only a single instance of that object exists in memory and reuses it each time it encounters a const constructor with the same parameters.
- The use of theme data for consistent styling across the app is a good practice. 
- The tests cover the main functionalities of the LoanForm widget, such as displaying the form and initial values, and changing the load amount and period with the sliders.
- The use of find functions to locate widgets in the widget tree is a good practice.

## Backend
- The code is DRY (Don't Repeat Yourself!), meaning the code seems to avoid unnecessary repetition.
- The code is well-structured and follows the MVC pattern, which makes it easy to understand and maintain.
- The use of custom exceptions for different error scenarios is a good practice. It makes error handling more precise and informative.
- The use of data transfer objects (DTOs) for request and response data is a good practice. It decouples the API layer from the service layer and makes the code more flexible.

### Areas for Improvement:

## Frontend
- The LoanForm widget is currently responsible for managing the form state, building the form UI, validating the form, and submitting the form to the API service. This could make the widget difficult to test, maintain, and reuse. Refactoring this widget to separate these concerns would greatly improve the code quality. Also, because of that this widget is not very open to extension without modification. If we want to change the validation logic or the way we handle API responses, we would need to modify the class directly. It could potentially be reused in other parts of the app, but it's tightly coupled to the ApiService and specific form fields, which limits its reusability.
- The tests could be made more robust by adding more assertions. For example, you could check that the sliders are initially at the correct positions, or that the form displays an error message when the input is invalid.
- The tests could be made more readable by extracting common setup code (like creating the LoanForm widget) into a setup function.
- It would be helpful to describe what each test is doing in the api_service_test file, currently there are no comments explaining the behaviour.

## Backend
- The DecisionEngine class seems to have multiple responsibilities (validating the personal ID code, calculating the credit modifier, and calculating the loan amount and period). This violates the Single Responsibility Principle (SRP) of SOLID. It would be better to separate these responsibilities into different classes.
- The DecisionEngineController directly uses the DecisionEngine service. This makes the controller tightly coupled with the service. It would be better to use dependency injection to inject the service into the controller. This would make the code more flexible and easier to test.

## Most Important Shortcoming of TICKET-101:

### Solution:

# TICKET-102 Implementation Plan
For TICKET-102, which involves implementing additional functionality for the decision engine, we propose the following plan:

## Requirements:
- Implement support for handling different segmentation scenarios based on personal codes.
- Ensure that the decision engine returns the maximum approved loan amount based on the segmentation and input parameters.
- Validate input parameters and handle edge cases gracefully.

## Implementation Steps:
1. **Analysis and Design**: Review the requirements and design the necessary changes to the decision engine architecture.
2. **Implementation**: Develop the logic to handle different segmentation scenarios and calculate the maximum approved loan amount accordingly.
3. **Testing**: Write unit tests to validate the new functionality and perform integration testing to ensure seamless integration with the existing codebase.
4. **Documentation**: Document the implemented changes, including any architectural decisions and usage instructions for future reference.

By following this plan, we aim to deliver a robust and scalable solution that meets the requirements of TICKET-102 and enhances the functionality of the decision engine.