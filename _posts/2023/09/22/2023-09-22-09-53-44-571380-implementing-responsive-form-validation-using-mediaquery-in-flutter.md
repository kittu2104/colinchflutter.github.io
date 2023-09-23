---
layout: post
title: "Implementing responsive form validation using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, formvalidation]
comments: true
share: true
---

When building a Flutter application, it is important to ensure that your forms provide a great user experience across different screen sizes. One aspect of this is validating user inputs in a responsive manner, where error messages are displayed appropriately depending on the screen size.

Flutter offers a powerful `MediaQuery` class that allows you to obtain information about the app's media, such as the screen size and orientation. By leveraging `MediaQuery`, we can easily implement responsive form validation in our Flutter app.

Here's an example of how you can achieve this:

1. **Import Required Packages**

   Start by importing the necessary packages in your Dart file:

   ```dart
   import 'package:flutter/material.dart';
   ```

2. **Create a Responsive Form Validation Widget**

   Create a new stateful widget that will represent your form validation screen:

   ```dart
   class ResponsiveFormValidationScreen extends StatefulWidget {
     @override
     _ResponsiveFormValidationScreenState createState() => _ResponsiveFormValidationScreenState();
   }
   
   class _ResponsiveFormValidationScreenState extends State<ResponsiveFormValidationScreen> {
     // Form validation logic goes here
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text("Form Validation"),
         ),
         body: Center(
           child: ListView(
             padding: EdgeInsets.all(16.0),
             children: [
               // Form widgets go here
             ],
           ),
         ),
       );
     }
   }
   ```

3. **Implement Responsive Validation Logic**

   Inside the `_ResponsiveFormValidationScreenState` class, you can define the logic to validate the form fields based on the screen size. For example, let's say you have a text field that requires a minimum length of 6 characters:

   ```dart
   bool isScreenLarge(BuildContext context) {
     return MediaQuery.of(context).size.width >= 600;
   }
   
   bool isFormValid(String value) {
     return value.length >= (isScreenLarge(context) ? 6 : 3);
   }
   ```

   Now, you can use this `isFormValid` function to determine whether the text field input is valid depending on the screen size.

4. **Display Validation Error Messages**

   Finally, based on the validation logic, you can display error messages to the user. For instance, if the input is less than the required length, show an error message below the input field:

   ```dart
   TextFormField(
     onChanged: (value) {
       setState(() {
         // Store the input value or call a validation function
         // Show error message based on the validation result
         _showErrorMessage(isFormValid(value) ? null : 'Minimum ${isScreenLarge(context) ? 6 : 3} characters required');
       });
     },
     // Other text field properties go here
   ),
   ```

   The `_showErrorMessage` function can be implemented to display the error message below the input field.

That's it! By using `MediaQuery` in Flutter, you can easily implement responsive form validation, creating a seamless user experience across different screen sizes.

#flutter #formvalidation