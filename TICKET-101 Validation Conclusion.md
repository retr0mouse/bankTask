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
- The use of find functions to locate widgets in the widget tree is a good practice.

## Backend
- The code is DRY (Don't Repeat Yourself!), meaning the code seems to avoid unnecessary repetition.
- The code is well-structured and follows the MVC pattern, which makes it easy to understand and maintain.
- The use of custom exceptions for different error scenarios is a good practice. It makes error handling more precise and informative.
- The use of data transfer objects (DTOs) for request and response data is a good practice. It decouples the API layer from the service layer and makes the code more flexible.

### Areas for Improvement:

## Frontend
- The LoanForm widget could benefit from more abstraction. For instance, the sliders for the loan amount and period could be extracted into their own widgets.
- The NationalIdTextForm widget could be more SOLID by introducing an abstraction for the validation logic. Currently, the validation logic is directly implemented in the widget. This could be refactored into a separate NationalIdValidator class, which would make the code more testable and maintainable.
- The NationalIdTextForm widget could benefit from more encapsulation. Currently, the validator property is publicly accessible and can be directly modified from outside the class. It would be better to make this property private and provide a public method for setting the validator.
- The NationalIdTextForm widget could also benefit from dependency inversion. Currently, it directly depends on the TextFormField class. This could be refactored to depend on an abstraction, which would make the code more flexible and easier to test.
- It would be helpful to describe what each test is doing in the api_service_test file, currently there are no comments explaining the behaviour.

## Backend
- The DecisionEngine class seems to have multiple responsibilities (validating the personal ID code, calculating the credit modifier, and calculating the loan amount and period). This violates the Single Responsibility Principle (SRP) of SOLID. It would be better to separate these responsibilities into different classes.
- The DecisionEngineController directly uses the DecisionEngine service. This makes the controller tightly coupled with the service. It would be better to use dependency injection to inject the service into the controller. This would make the code more flexible and easier to test.

## Most Important Shortcoming of TICKET-101:
- The text under the loan period slider is showing '6 months' a the end of the slider, when in reality it should show '12 months' 
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
