![Logo of the project]([https://raw.githubusercontent.com/gditoro/certo/refs/heads/main/Certo%20Validation%20Logo.png])
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
