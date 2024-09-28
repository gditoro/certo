![Logo of the project](https://raw.githubusercontent.com/gditoro/certo/refs/heads/main/Certo%20Validation%20Logo.png)
### Certo: Form Validation
> A flexible form validation library for JavaScript applications with the powerful `Regra` validation rule notation.

---

### Validation Rule Notation Premise:

The validation rule notation should provide a clean, readable format for defining validation rules that are flexible and support a wide range of inputs, logic, and conditions. Here's how it works:

---

### 1. **Rule Syntax**:
- **Multiple Inputs**: Inputs are referenced using `#inputId`. Their values are accessed via `.val` (e.g., `#inputId.val`).
- **Current Input**: The current input being validated can be referenced as `$` or `$me`.
- **Variables**: Declared with `%{variableName, value}` and referenced as `%variableName`.
- **Error Messages**: Defined for each rule with the format `{rule: "Error message"}`.

### 2. **Rule Grouping and Combination**:
- Multiple rules can be grouped within square brackets `[]`, with each rule separated by semicolons (`;`).
- Logical operators (`&&`, `||`, `!`) can be used for complex conditions inside curly braces `{}`.
- Arithmetic, comparison, and assignment operators (`+`, `-`, `*`, `/`, `=`, `==`, `!=`, `>`, `<`, `>=`, `<=`) are supported.

### 3. **Built-In Validation Functions**:

**General Validators**:
- **`required(value)`**: Ensures the field is not empty.
- **`isNumber(value)`**: Validates if the value is a valid number.
- **`isInteger(value)`**: Checks if the value is an integer.
- **`isFloat(value)`**: Checks if the value is a floating-point number.
- **`isBoolean(value)`**: Validates if the value is a boolean (`true` or `false`).
- **`isEmail(value)`**: Validates if the value is a properly formatted email.
- **`isUrl(value)`**: Ensures the value is a valid URL.

**Length and Size Validators**:
- **`minLength(value, min)`**: Validates that the value has at least `min` characters.
- **`maxLength(value, max)`**: Validates that the value has at most `max` characters.
- **`lengthBetween(value, min, max)`**: Ensures the value length is between `min` and `max`.
- **`minSize(value, min)`**: Ensures the numerical value is greater than or equal to `min`.
- **`maxSize(value, max)`**: Ensures the numerical value is less than or equal to `max`.
- **`sizeBetween(value, min, max)`**: Ensures the numerical value falls between `min` and `max`.

**String and Pattern Validators**:
- **`matchesRegex(value, pattern)`**: Validates that the value matches the given regular expression.
- **`isAlpha(value)`**: Checks if the value contains only alphabetic characters.
- **`isAlphanumeric(value)`**: Validates that the value contains only alphabetic and numeric characters.
- **`isUpperCase(value)`**: Checks if the value is in uppercase.
- **`isLowerCase(value)`**: Ensures the value is in lowercase.
- **`contains(value, substring)`**: Ensures the value contains a specific substring.

**Date and Time Validators**:
- **`isDate(value)`**: Validates that the value is a valid date.
- **`isTime(value)`**: Validates if the value is a valid time.
- **`isAfter(value, date)`**: Checks if the value is a date after the specified `date`.
- **`isBefore(value, date)`**: Ensures the value is a date before the given `date`.
- **`isDateBetween(value, startDate, endDate)`**: Ensures the value is a date between `startDate` and `endDate`.

**Custom Logical Functions**:
- **`isEmpty(value)`**: Checks if the field is empty.
- **`isNotEmpty(value)`**: Ensures the field is not empty.
- **`equals(value, compareTo)`**: Validates if the value equals `compareTo`.
- **`notEquals(value, compareTo)`**: Ensures the value does not equal `compareTo`.

**File Validators**:
- **`isFileType(value, fileType)`**: Ensures the uploaded file is of a specified type (e.g., `image/png`).
- **`fileSizeBetween(value, minSize, maxSize)`**: Validates that the uploaded file's size is between `minSize` and `maxSize`.

**Mathematical Validators**:
- **`greaterThan(value, threshold)`**: Ensures the value is greater than `threshold`.
- **`lessThan(value, threshold)`**: Ensures the value is less than `threshold`.
- **`between(value, min, max)`**: Validates that the value falls between `min` and `max`.
- **`multipleOf(value, base)`**: Ensures the value is a multiple of the `base`.

---

### 4. **Examples**:

#### Simple Required and Minimum Length:
```js
[
  {required: "This field is required"};
  {minLength($.val, 5): "Minimum length is 5 characters"}
]
```

#### Complex Range Validation Based on Other Inputs:
```js
%{minValue, 10 | maxValue, #input1.val + 20} ?
{#input2.val > %minValue && #input2.val < %maxValue: "Value must be between 10 and #input1.val + 20"} :
{#input2.val > 5: "Value must be greater than 5"}
```

#### Conditional Validation with Multiple Rules:
```js
[
  {required};
  {isNumber($.val)};
  {between($.val, 1, 100): "Value must be between 1 and 100"}
]
```

---

### 5. **Advanced Examples**:

#### Nested Logic with Arithmetic Operations:
```js
%{threshold, 10} ?
{$.val > %threshold && #input2.val < #input3.val: "Value must exceed 10 and be less than #input3.val"} :
{#input2.val > 5: "Value must be greater than 5"}
```

#### Validating File Uploads:
```js
[
  {isNotEmpty($.val): "File is required"};
  {isFileType($.val, "image/png"): "Only PNG files are allowed"};
  {fileSizeBetween($.val, 1024, 1048576): "File size must be between 1KB and 1MB"}
]
```

#### Dynamic Date Validation:
```js
{isDate($.val) && isAfter($.val, $today): "Date must be valid and in the future"}
```

---

### 6. **Conclusion**:

The validation rule notation provides a powerful and flexible way to define validation rules for various types of inputs. By combining simple syntax with advanced features, developers can create complex validation logic with ease. This notation aims to simplify the process of defining and managing validation rules, making it easier to maintain and update validation logic in web applications.


---

![Logo of the project](https://raw.githubusercontent.com/gditoro/certo/refs/heads/main/Certo%20Validation%20Logo.png)

### Certo: Form Validation
> A flexible form validation library for JavaScript applications with the powerful `Regra` validation rule notation.

---

### Validation Rule Notation Premise:

The validation rule notation provides a clean, readable format for defining validation rules that are flexible and powerful. With automatic variable declarations and interpolation, it supports a wide range of validation cases while keeping the syntax concise.

---

### 1. **Rule Syntax**:

- **Input References**:
  - Inputs are referenced by `#inputId`. Their values are accessed via `.val`, like `#inputId.val`.
  - The current input being validated can be referenced as `$` or `$me` without needing `#inputId.val` for each rule.

- **Automatic Variable Declarations**:
  - When using built-in validation functions, variables such as `%min`, `%max`, etc., are automatically declared based on the function's parameters.
  - These variables are instantly available for use in error messages without needing to explicitly declare them.

- **Error Message Interpolation**:
  - Error messages can automatically interpolate the variables declared from validation functions. For example, `minLength:5` automatically creates `%min=5`, which is available for error messages.
  - Placeholders in error messages follow the `%variableName` format (e.g., `%min`, `%max`, etc.).

---

### 2. **Rule Grouping and Combination**:

- **Multiple Rules**:
  - Group rules inside square brackets `[]`, separating them with semicolons (`;`).
  - Logical operators (`&&`, `||`, `!`) can be used for complex conditions within curly braces `{}`.

- **Automatic Message Handling**:
  - Messages tied to rules are declared directly after the rule, simplifying the notation. For instance, `minLength:5 -> "Minimum length is %min characters."`

---


### 3. **Built-In Validation Functions**:

#### **General Validators**:
- **`required()`**: Ensures the field is not empty.
- **`isBoolean()`**: Validates if the value is a boolean (`true` or `false`).
- **`isDate()`**: Validates that the value is a valid date.
- **`isEmail()`**: Checks for a valid email format.
- **`isFloat()`**: Checks if the value is a floating-point number.
- **`isInteger()`**: Checks if the value is an integer.
- **`isNumber()`**: Validates if the value is a number.
- **`isTime()`**: Validates if the value is a valid time.
- **`isUrl()`**: Ensures the value is a valid URL.
- **`isAlpha()`**: Checks if the value contains only alphabetic characters.
- **`isAlphanumeric()`**: Validates that the value contains only alphabetic and numeric characters.
- **`matchesRegex(pattern)`**: Validates that the value matches the given regular expression.

#### **Length and Size Validators**:
- **`minLength(min)`**: Requires at least `min` characters. Automatically declares `%min`.
- **`maxLength(max)`**: Requires no more than `max` characters. Automatically declares `%max`.
- **`lengthBetween(min, max)`**: Validates that length is between `min` and `max`. Automatically declares `%min` and `%max`.
- **`minSize(min)`**: Ensures the numerical value is at least `min`.
- **`maxSize(max)`**: Ensures the numerical value is at most `max`.
- **`sizeBetween(min, max)`**: Ensures the numerical value is between `min` and `max`.
- **`fileSizeBetween(minSize, maxSize)`**: Validates that the uploaded file's size is between `minSize` and `maxSize`.
- **`isFileType(fileType)`**: Ensures the uploaded file is of the specified type.

#### **Logical Validators**:
- **`allOf(...rules)`**: Ensures all rules are true.
- **`anyOf(...rules)`**: Ensures at least one rule is true.
- **`noneOf(...rules)`**: Ensures none of the rules are true.

#### **Date and Time Validators**:
- **`isAfter(date)`**: Ensures the date is after `date`.
- **`isBefore(date)`**: Ensures the date is before `date`.
- **`isFutureDate()`**: Ensures the date is in the future.
- **`isPastDate()`**: Ensures the date is in the past.
- **`maxDate(date)`**: Ensures the date is before or equal to `date`.
- **`minDate(date)`**: Ensures the date is after or equal to `date`.
- **`isAfterTime(time)`**: Ensures the time is after `time`.
- **`isBeforeTime(time)`**: Ensures the time is before `time`.
- **`isFutureTime()`**: Ensures the time is in the future.
- **`isPastTime()`**: Ensures the time is in the past.
- **`maxTime(time)`**: Ensures the time is before or equal to `time`.
- **`minTime(time)`**: Ensures the time is after or equal to `time`.
- **`dateBetween(startDate, endDate)`**: Ensures the date is between `startDate` and `endDate`.
- **`timeBetween(startTime, endTime)`**: Ensures the time is between `startTime` and `endTime`.

#### **Mathematical Validators**:
- **`greaterThan(threshold)`**: Ensures the value is greater than `threshold`. Automatically declares `%threshold`.
- **`lessThan(threshold)`**: Ensures the value is less than `threshold`.
- **`multipleOf(base)`**: Ensures the value is a multiple of `base`.
- **`maxNum(max)`**: Ensures the numerical value is at most `max`.
- **`minNum(min)`**: Ensures the numerical value is at least `min`.
- **`numBetween(min, max)`**: Ensures the numerical value is between `min` and `max`.

#### **String and Pattern Validators**:
- **`contains(substring)`**: Ensures the value contains a specific substring.
- **`isLowerCase()`**: Ensures the value is in lowercase.
- **`isUpperCase()`**: Ensures the value is in uppercase.
- **`wordsBetween(min, max)`**: Ensures the number of words is between `min` and `max`.
- **`wordsMax(max)`**: Ensures the number of words is at most `max`.
- **`wordsMin(min)`**: Ensures the number of words is at least `min`.

#### **Custom Logical Functions**:
- **`equals(compareTo)`**: Validates if the value equals `compareTo`.
- **`notEquals(compareTo)`**: Ensures the value does not equal `compareTo`.
- **`isEmpty()`**: Checks if the field is empty.
- **`isNotEmpty()`**: Ensures the field is not empty.

---

### 4. **Examples**:

#### Simple Required and Minimum Length:
```js
[
  required -> "This field is required.";
  minLength:5 -> "Minimum length is %min characters."
]
```

- **Explanation**:
  - `minLength:5` automatically assigns `%min=5`, and the error message interpolates this value.

#### Complex Range Validation Based on Other Inputs:
```js
[
  required -> "This field is required.";
  betweenLength:5, 20 -> "Length must be between %min and %max characters."
]
```

- **Explanation**:
  - `betweenLength:5,20` automatically assigns `%min=5` and `%max=20`. These variables are used in the error message.

#### Conditional Validation with Multiple Rules:
```js
[
  required;
  isNumber;
  between:1, 100 -> "Value must be between %min and %max."
]
```

- **Explanation**:
  - `between:1,100` auto-declares `%min=1` and `%max=100` for use in the message.

---

### 5. **Advanced Examples**:

#### Nested Logic with Automatic Variables:
```js
%{threshold=10} ?
{$.val > %threshold && #input2.val < #input3.val -> "Value must exceed %threshold and be less than #input3.val."} :
{#input2.val > 5 -> "Value must be greater than 5."}
```

- **Explanation**:
  - The `threshold=10` is declared once, used in multiple rules. Interpolation occurs naturally.

#### Validating File Uploads:
```js
[
  required -> "File is required.";
  isFileType:"image/png" -> "Only PNG files are allowed.";
  fileSizeBetween:1024, 1048576 -> "File size must be between 1KB and 1MB."
]
```

- **Explanation**:
  - Variables like file size (`%min`, `%max`) are automatically inferred for use in the error message.

#### Dynamic Date Validation:
```js
isDate && isAfter:$today -> "Date must be valid and in the future."
```

- **Explanation**:
  - Auto-interpolation of the current date is handled within the `isAfter` rule.

---

### 6. **Conclusion**:

The updated `Regra` validation notation offers a powerful yet concise way to define complex validation rules. With automatic variable declarations and error message interpolation, Certo allows for clear and flexible validation logic that is easy to manage.
