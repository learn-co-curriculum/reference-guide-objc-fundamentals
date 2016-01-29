# Reference Guide: Objective-C Fundamentals

## Table of Contents

* [NSLog Basics](#nslog-basics)
  * [String Literal](#string-literal)
  * [Format String](#format-string)
  * [Format Specifiers](#format-specifiers)
* [Primitives](#primitives)
  * [Common Primitives](#common-primitives)
  * [Declaring A Primitive Variable](#declaring-a-primitive-variable)
  * [Redefining A Primitive Variable](#redefining-a-primitive-variable)
  * [Printing A Primitive Variable](#printing-a-primitive-variable)
* [Operators](#operators)
  * [Mathematical Operators](#mathematical-operators)
  * [Assignment Operators](#assignment-operators)
  * [Comparison Operators](#comparison-operators)
  * [Operation Precedence](#operation-precedence)
* [Calling Methods](#calling-methods)
  * [Method Call Syntax](#method-call-syntax)
  * [Method Call Anatomy](#method-call-anatomy)
* [NSString](#nsstring)
  * [String Literal](#string-literal)
  * [Introspection Methods](#introspection-methods)
  * [Comparing Strings](#comparing-strings)
  * [Case Change Methods](#case-change-methods)
  * [Interpolation And Concatenation Methods](#interpolation-and-concatenation-methods)


## NSLog Basics

### String Literal

```objc
NSLog(@"Hello, World!");
```

This will print:

```
Hello, World!
```

### Format String

```objc
NSLog(@"%@, %@!", @"Hello", @"World");
NSLog(@"There are %li lights.", 4);
```
This will print:

```
Hello, World!
There are 4 lights.
```

### Format Specifiers

| Type         | Format Specifier |
|:------------:|:----------------:|
| `NSString`   | `%@`
| `NSInteger`  | `%li`            |
| `NSUInteger` | `%lu`            |
| `CGFloat`    | `%f` or `%.nf`, *where* `n` *is the number of decimal places to display* |
| `BOOL`       | `%d`             |

Examples:

```objc
NSLog(@"%@", @"Welcome!");
NSLog(@"-1: %li", -1);
NSLog(@"42: %lu", 42);
NSLog(@"pi: %f", 3.141593);
NSLog(@"sqrt2: %.12f", 1.41421356237);
NSLog(@"yes: %d", YES);
```
These will print:

```
Welcome!
-1: -1
42: 42
pi: 3.141593
sqrt2: 1.414213562370
yes: 1
```

[Back to Top](#table-of-contents)
## Primitives

### Common Primitives

| Primitive   | Description |
|:-----------:|:------------|
| `NSInteger` | An integer value that can be either positive or negative. |
| `NSUInteger`| An integer value that can **only** be zero or positive (the "U" means "unsigned"). |
| `CGFloat`   | A "float" value that can (imperfectly) hold a decimal point. **Note:** *Do not use float values to hold currency.* |
| `BOOL`      | A `YES` or `NO` value: `0` means "no", `1` means "yes" |

### Declaring A Primitive Variable

Syntax:

```objc
Type variableName = value;
```

Examples:

```objc
NSInteger i = 0;
NSUInteger u = 0;
CGFloat f = 0.0;
BOOL hidden = NO;
```
**Reminder:** *Do not use a* `*` *when declaring primitives. Assigning an integer to* `NSInteger *` *will cause the compiler to generate an* `invalid integer to pointer conversion` *warning. The same goes for declaring any of the data types. This syntax does serve a purpose so the language permits it, but your application won't do what you expect.*

### Redefining A Primitive Variable

Syntax:

```objc
variableName = value;
```

Examples:

```objc
i = -1;
u = 1;
f = 3.14159265359;
hidden = YES;
```

### Printing A Primitive Variable

See [Format Specifiers](#format-specifiers).

Examples:

```objc
NSLog(@"i: %li", i);
NSLog(@"u: %lu", u);
NSLog(@"f: %f", f);
NSLog(@"f: %.12f", f);
NSLog(@"hidden: %d", hidden);
```

This will print:

```
i: -1
u: 1
f: 3.141593
f: 3.141592653590
hidden: 1           // 1 means 'yes'
```
[Back to Top](#table-of-contents)
## Operators

### Mathematical Operators

| Operator | Name               | Pronunciation | Description |
|:--------:|:-------------------|:--------------|:------------|
| `+` | Addition Operator       | "plus" or "add"       | Results to the value that is the **sum** of the two operands. |
| `-` | Subtraction Operator    | "minus" or "subtract" | Results to the **difference** of subtracting the right operand from the left operand.  |
| `*` | Multiplication Operator | "star" or "times"     | Results to the **product** of multiplying the two operands. |
| `/` | Division Operator       | "slash" or "over"     | Results to the **quotient** of dividing the left operand by the right operand. **Note:** *This operator truncates integer-only divisions.* |
| `%` | **Advanced:** Modulus or Modulo       | "modulus" or "modulo" | Results to the **remainder** of dividing the left operand by the right operand. **Note:** *This does not perform the strict mathematical definition of modulus.* |

**Note:** *Exponent calculations are performed using the* `pow()` *function from C's* `math.h` *library.*

Example:

```objc
NSInteger i = 5 + 7;
NSLog(@"i: %li", i);
```
This will print: `i: 12`.

### Increment and Decrement Operators

| Symbol | Name               | Pronunciation | Description |
|:------:|:-------------------|:--------------|:------------|
| `++`   | Increment Operator | "plus-plus"   | Increases the value of the associated variable by `1`.
| `--`   | Decrement Operator | "minus-minus" | Decreases the value of the associated variable by `1`.

Example:

```objc
NSUInteger i = 0;
i++;
NSLog(@"i: %lu", i);
```
This will print: `i: 1`.

### Comparison Operators

| Comparison | Pronunciation              | Description |
|:----------:|:---------------------------|:------------|
| `==` | "is equal to" or "double equals" | Results to `YES` only if the two operands are **exactly** equal in value. |
| `!=` | "is not equal to"                | Results to `YES` only if the two operands are **not exactly** equal in value.
| `<`  | "less than"                      | Results to `YES` only if the value of the left operand is lower than the value of the right operand. |
| `<=` | "less-than-or-equal-to"          | Results to `YES` if the value of the left operand is lower than or the same as the value of the right operand.
| `>`  | "greater than"                   | Results to `YES` if the value of the left operand is higher than the value of the right operand.
| `>=` | "greater-than-or-equal-to"       | Results to `YES` if the value of the left operand is higher than or the same as the value of the right operand.

Example:

```objc
BOOL sevenIsEqualToSeven = 7 == 7;
NSLog(@"7 == 7: %d", sevenIsEqualToSeven);
```
This will print: `7 == 7: 1`, meaning 'yes'.

### Operation Precedence

Priority | Operators 
---------|-----------------------------
Highest  | `()` precedence override 
         | `++` `--`
         | `*` `/` `%`
         | `+` `-`
         | `<` `<=` `>` `>=`
         | `==` `!=`
Lowest   | `=` `+=` `-=` `*=` `/=` `%=`

**Top-tip:** *Most of the time you can simply follow the [PEMDAS](http://math.wikia.com/wiki/P.E.M.D.A.S) acronym.*

Example:

```objc
NSInteger x = 7 + 8 * (9 - 3);
NSLog(@"x: %li", x);
```
This will print: `x: 55`.

[Back to Top](#table-of-contents)
## Calling Methods

### Method Call Syntax

Full Syntax:

```objc
ReturnType *captureVariable = [recipientObject methodNameArgument:argumentValue];
```

Example:

```objc
NSString *welcome = [@"Welcome" stringByAppendingString:@"!"];

NSLog(@"%@", welcome);
```
This will print: `Welcome!`.

Syntax without arguments:

```objc
ReturnType *captureVariable = [recipientObject methodName];
```

Example:

```objc
NSString *uppercase = [@"welcome!" uppercaseString];

NSLog(@"%@", uppercase);
```
This will print: `WELCOME!`.


### Method Call Anatomy

Methods are behaviors that an object can perform (primitives cannot receive method calls, but they *can* be method arguments).

| Component        | Description |
|:----------------:|:------------|
| Return Type      | The kind of variable that the method will result to, if any.
| Capture Variable | The name of the variable to save the method's result into; this can be a new variable or an existing variable, but it must match the return type of the method.
| Recipient Object (*also* "Receiver" *or* "Target") | The object on which the method is being called, which should perform the expected behavior.
| Method Name (*also* "Selector" *or* "Message") | The name of the method which should describe its effect and which is used to call its behavior. The method name may contain argument specifiers.
| Arguments (*also* "Parameters") | Variables or values be passed into the method which are relevant to its operation, and which the method requires in order to run.

[Back to Top](#table-of-contents)
## `NSString`

### String Literal

Strings are text values held as objects. The string literal `@""` creates and returns an `NSString` instance with the text value that is entered between its double quotes (`"`):

```objc
NSString *welcome = @"Welcome!";

NSLog(@"%@", welcome);
``` 
This will print: `Welcome!`.

### Introspection Methods

#### `length`

This method returns an `NSUInteger` value equal to the number of characters in the recipient string. This method counts up from `1` and will always be one higher than the index of the string's final character (since the index starts at `0`).

```objc
NSUInteger welcomeLength = [@"welcome." length];

NSLog(@"welcomeLength: %lu", welcomeLength);
```
This will print: `welcomeLength: 8`.

#### `hasPrefix:`

This method returns a `BOOL` that contains `YES` if the recipient string begins with the substring matching the argument string.

```objc
BOOL doctor = [@"Doctor Who" hasPrefix:@"Doctor"];

NSLog(@"doctor: %d", doctor);
```
This will print: `doctor: 1`.

#### `hasSuffix:`

This method returns a `BOOL` that contains `YES` if the recipient string ends with the substring matching the argument string.

```objc
BOOL esquire = [@"John Smith, Esq." hasSuffix:@"Esq."];

NSLog(@"esquire: %d", esquire);
```
This will print: `esquire: 1`.

### Comparing Strings

#### `isEqualToString:`

Use the `isEqualToString:` method to check strings for equivalence. This method returns a `BOOL` that is `YES` only if the recipient string **exactly** matches the argument string.

Examples:

```objc
// the strings are exactly alike

if ([@"Sparta" isEqualToString:@"Sparta"]) {
    NSLog(@"This is Sparta!");
}
```
This will print: `This is Sparta!`.

```objc
// the strings are NOT exactly alike

if ([@"snoop dog" isEqualToString:@"Snoop Dog"]) {
    NSLog(@"This will not print.");
} else {
    NSLog(@"Will the real Snoop Dog please stand up?");
}
```
This will print: `Will the real Snoop Dog please stand up?`.

### Case Change Methods

#### `uppercaseString`

This method returns a new string that is the uppercase form of the recipient string. This method does **not** affect non-letter characters such as digits and punctuation.

```objc
NSString *welcome = [@"welcome." uppercaseString];

NSLog(@"%@", welcome);
```
This will print: `WELCOME.`.

#### `lowercaseString`

This method returns a new string that is the lowercase form of the recipient string. This method does **not** affect non-letter characters such as digits and punctuation.

```objc
NSString *welcome = [@"WELCOME!" lowercaseString];

NSLog(@"%@", welcome);
```
This will print: `welcome!`.

#### `capitalizedString`

This method returns a new string that is the *title case* form of the recipient string. This means that the first letter of each separate word in the recipient string will be uppercased in the returned string. This method does **not** affect non-letter characters such as digits and punctuation.

```objc
NSString *welcomeToFlatiron = [@"welcome to flatiron." capitalizedString];

NSLog(@"%@", welcomeToFlatiron);
```
This will print: `Welcome To Flatiron.`.

### Interpolation And Concatenation Methods

#### `stringWithFormat:`

The `stringWithFormat:` method is a class method that returns the *interpolated string* generated from the format string and its format arguments that are submitted together as the one method argument. As a class method, this method must be called on `NSString` as the recipient object:

```objc
NSString *welcome = [NSString stringWithFormat:@"%@ %@ %@!", @"Welcome", @"to", @"Flatiron"];

NSLog(@"%@", welcome);
```
This will print: `Welcome to Flatiron!`.

String formatting uses the same [Format Specifiers](#format-specifiers) as `NSLog()`.

#### `stringByAppendingString:`

This is an instance method that returns a **new** string that is the *concatenation* of the recipient string and the argument string. As an instance method, this must be called on an existing string variable:

```objc
NSString *welcome = @"Welcome";
NSString *welcomeBang = [welcome stringByAppendingString:@"!"];

NSLog(@"%@", welcomeBang);
```
This will print: `Welcome!`.

#### `stringByAppendingFormat:`

This is an instance method that returns a **new** string that is the *concatenation* of the recipient string with the *interpolated string* that is generated from the format string and its format arguments that are submitted together as the one method argument. As an instance method, this method must be called on an existing string variable:

```objc
NSString *welcome = @"Welcome";
NSString *welcomeToFlatiron = [welcome stringByAppendingFormat:@" %@ %@!", @"to", @"Flatiron"];

NSLog(@"%@", welcomeToFlatiron);
```
This will print: `Welcome to Flatiron!`.

String formatting uses the same [Format Specifiers](#format-specifiers) as `NSLog()`.

[Back to Top](#table-of-contents)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/reference-guide-objc-fundamentals' title='Reference Guide: Objective-C Fundamentals'>Reference Guide: Objective-C Fundamentals</a> on Learn.co and start learning to code for free.</p>
