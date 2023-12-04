### File Description

This Rust file appears to define an exception handling mechanism for a program, likely within a broader project related to a stack-based system (`crate::stack`). The code defines several structures and macros to handle exceptions, providing functionalities to create, format, and handle exceptions.

### Symbols

#### Enums

1. **`ExceptionType`**
   - **Methods:**
     - `is_normal_termination() -> Option<i32>`: Checks if the exception is a normal termination, returning the corresponding code.
     - `exception_code() -> Option<ExceptionCode>`: Retrieves the exception code if it's of type `System`.
     - `custom_code() -> Option<i32>`: Retrieves the custom exception code if it's of type `Custom`.
     - `exception_or_custom_code() -> i32`: Returns either the exception code or custom code.
     - `exception_message() -> String`: Generates a human-readable exception message.

#### Structs

2. **`Exception`**
   - **Fields:**
     - `exception: ExceptionType`: The type of exception (system or custom).
     - `value: StackItem`: The associated value with the exception.
     - `file: &'static str`: The file where the exception occurred.
     - `line: u32`: The line number in the file where the exception occurred.
   - **Methods:**
     - `from_code(code: ExceptionCode) -> Self`: Creates an exception from a system exception code.
     - `from_code_and_value(code: ExceptionCode, value: impl Into<IntegerData>, file: &'static str, line: u32) -> Self`: Creates an exception with a system exception code and a value.
     - `from_number_and_value(number: usize, value: StackItem, file: &'static str, line: u32) -> Self`: Creates a custom exception with a number and a value.
     - `exception_code() -> Option<ExceptionCode>`: Retrieves the exception code if it's of type `System`.
     - `custom_code() -> Option<i32>`: Retrieves the custom exception code if it's of type `Custom`.
     - `exception_or_custom_code() -> i32`: Returns either the exception code or custom code.
     - `is_normal_termination() -> Option<i32>`: Checks if the exception is a normal termination.
     - `fmt(&self, f: &mut fmt::Formatter) -> fmt::Result`: Formats the exception for display.
   - **Implementations:**
     - `From<ExceptionCode> for Exception`: Implements conversion from `ExceptionCode` to `Exception`.
     - `fmt::Display for Exception`: Implements the display format for `Exception`.
     - `fmt::Debug for Exception`: Implements the debug format for `Exception`.

#### Type Aliases

3. **Result Types**
   - `ResultMut<'a, T> = Result<&'a mut T>`
   - `ResultOpt<T> = Result<Option<T>>`
   - `ResultRef<'a, T> = Result<&'a T>`
   - `ResultVec<T> = Result<Vec<T>>`
   - `Status = Result<()>`

#### Macros

4. **`exception!`**
   - A macro for generating exceptions with various parameters such as code, value, message, file, and line.

5. **`err!`**
   - A macro for returning an `Err` result with an associated exception.

6. **`custom_err!`**
   - A custom error macro for returning an `Err` result with a custom exception.

### How the Code Works

- **ExceptionType Enum:**
  - Represents the type of exceptions, distinguishing between system exceptions (`ExceptionCode`) and custom exceptions (arbitrary integer codes).
  - Provides methods to retrieve codes, check for normal termination, and generate exception messages.

- **Exception Struct:**
  - Represents an exception instance with details such as type, associated value, file, and line number.
  - Implements methods to create exceptions, retrieve codes, check termination, and format for display.

- **Macros:**
  - `exception!`: Simplifies the creation of exceptions with different parameters.
  - `err!`: Constructs an `Err` result with an associated exception.
  - `custom_err!`: Constructs an `Err` result with a custom exception.

- **Result Types:**
  - Defines several type aliases for `Result` with specific types, such as mutable reference, option, reference, vector, and unit.

This code seems to provide a flexible and standardized way of handling exceptions in the context of the larger project. It leverages Rust's enums, structs, and macros to encapsulate and manage exception-related logic.


***


Certainly! Let's delve deeper into the code, going method by method and macro by macro.

#### `ExceptionType` Enum

1. **`is_normal_termination() -> Option<i32>`:**
   - Checks if the exception is a normal termination or custom termination.
   - Returns the termination code if it is normal termination, otherwise, returns `None`.

2. **`exception_code() -> Option<ExceptionCode>`:**
   - Retrieves the exception code if the exception type is `System`.

3. **`custom_code() -> Option<i32>`:**
   - Retrieves the custom exception code if the exception type is `Custom`.

4. **`exception_or_custom_code() -> i32`:**
   - Returns either the exception code or the custom code, depending on the type of exception.

5. **`exception_message() -> String`:**
   - Generates a human-readable exception message including the exception code or custom code.

#### `Exception` Struct

1. **`from_code(code: ExceptionCode) -> Self`:**
   - Creates an `Exception` from a system exception code.
   - Uses the associated macro to set the file and line to the current file and line.

2. **`from_code_and_value(code: ExceptionCode, value: impl Into<IntegerData>, file: &'static str, line: u32) -> Self`:**
   - Creates an `Exception` with a system exception code and a value.
   - Converts the value into `IntegerData` and sets other fields accordingly.

3. **`from_number_and_value(number: usize, value: StackItem, file: &'static str, line: u32) -> Self`:**
   - Creates a custom `Exception` with a number and a value.
   - Uses the number as a custom code.

4. **`exception_code() -> Option<ExceptionCode>`:**
   - Delegates to the inner `ExceptionType` for getting the exception code.

5. **`custom_code() -> Option<i32>`:**
   - Delegates to the inner `ExceptionType` for getting the custom code.

6. **`exception_or_custom_code() -> i32`:**
   - Delegates to the inner `ExceptionType` for getting either the exception code or custom code.

7. **`is_normal_termination() -> Option<i32>`:**
   - Delegates to the inner `ExceptionType` for checking if it's normal termination.

8. **`fmt(&self, f: &mut fmt::Formatter) -> fmt::Result`:**
   - Formats the exception for display.
   - Includes the exception message, associated value, file, and line.

#### Macros

1. **`exception!` Macro:**
   - A flexible macro for generating exceptions.
   - Can be called with various combinations of parameters like code, value, message, file, and line.
   - Uses the `TvmError::TvmExceptionFull` error variant.

2. **`err!` Macro:**
   - A macro for returning an `Err` result with an associated exception.
   - Calls the `exception!` macro and wraps it in an `Err`.

3. **`custom_err!` Macro:**
   - A custom error macro for returning an `Err` result with a custom exception.
   - Creates an exception with a custom code and other details and wraps it in an `Err`.

#### Result Types

1. **`ResultMut<'a, T> = Result<&'a mut T>`:**
   - A specific type alias for a mutable reference within a `Result`.

2. **`ResultOpt<T> = Result<Option<T>>`:**
   - A specific type alias for a `Result` with an `Option` type.

3. **`ResultRef<'a, T> = Result<&'a T>`:**
   - A specific type alias for a reference within a `Result`.

4. **`ResultVec<T> = Result<Vec<T>>`:**
   - A specific type alias for a `Result` with a `Vec` type.

5. **`Status = Result<()>`:**
   - A specific type alias for a `Result` with an empty tuple, representing success or failure without any additional information.

### Summary

The code provides a comprehensive and modular exception handling system. It defines structures and macros to encapsulate the creation, formatting, and handling of exceptions. The use of enums, structs, and macros helps keep the code clean and flexible, allowing developers to handle exceptions in a standardized way within their project. The macros further simplify the process of creating and returning exceptions, enhancing the readability of the code where exceptions are raised and handled.




***


Certainly! Let's break down each entity in the code with more detailed explanations.

### 1. `ExceptionType` Enum

#### Methods:

- **`is_normal_termination() -> Option<i32>`:**
  - Checks if the exception is a normal termination or custom termination.
  - Returns `Some(0)` for normal termination, `Some(1)` for alternative termination, and `None` for other cases.

- **`exception_code() -> Option<ExceptionCode>`:**
  - Retrieves the system exception code if the exception type is `System`.
  - Returns `None` if the exception type is `Custom`.

- **`custom_code() -> Option<i32>`:**
  - Retrieves the custom exception code if the exception type is `Custom`.
  - Returns `None` if the exception type is `System`.

- **`exception_or_custom_code() -> i32`:**
  - Returns either the system exception code or custom exception code as an `i32`.
  
- **`exception_message() -> String`:**
  - Generates a human-readable exception message.
  - For system exceptions, it includes the exception code and its corresponding u8 value.
  - For custom exceptions, it includes only the custom code.

### 2. `Exception` Struct

#### Fields:

- **`exception: ExceptionType`:**
  - The type of exception, either `System` or `Custom`.

- **`value: StackItem`:**
  - The associated value with the exception, presumably representing some data on the stack.

- **`file: &'static str`:**
  - The file where the exception occurred. Captured using the `file!()` macro.

- **`line: u32`:**
  - The line number in the file where the exception occurred. Captured using the `line!()` macro.

#### Methods:

- **`from_code(code: ExceptionCode) -> Self`:**
  - Creates an `Exception` from a system exception code.
  - Uses the associated macro to set the file and line to the current file and line.

- **`from_code_and_value(code: ExceptionCode, value: impl Into<IntegerData>, file: &'static str, line: u32) -> Self`:**
  - Creates an `Exception` with a system exception code and a value.
  - Converts the value into `IntegerData` and sets other fields accordingly.

- **`from_number_and_value(number: usize, value: StackItem, file: &'static str, line: u32) -> Self`:**
  - Creates a custom `Exception` with a number and a value.
  - Uses the number as a custom code.

- **`exception_code() -> Option<ExceptionCode>`:**
  - Delegates to the inner `ExceptionType` for getting the exception code.

- **`custom_code() -> Option<i32>`:**
  - Delegates to the inner `ExceptionType` for getting the custom code.

- **`exception_or_custom_code() -> i32`:**
  - Delegates to the inner `ExceptionType` for getting either the exception code or custom code.

- **`is_normal_termination() -> Option<i32>`:**
  - Delegates to the inner `ExceptionType` for checking if it's normal termination.

- **`fmt(&self, f: &mut fmt::Formatter) -> fmt::Result`:**
  - Formats the exception for display.
  - Includes the exception message, associated value, file, and line.

### 3. Macros

#### `exception!` Macro

- A flexible macro for generating exceptions.
- It can be called with various combinations of parameters like code, value, message, file, and line.
- Uses the `TvmError::TvmExceptionFull` error variant.

#### `err!` Macro

- A macro for returning an `Err` result with an associated exception.
- Calls the `exception!` macro and wraps it in an `Err`.

#### `custom_err!` Macro

- A custom error macro for returning an `Err` result with a custom exception.
- Creates an exception with a custom code and other details and wraps it in an `Err`.

### 4. Result Types

#### Type Aliases:

- **`ResultMut<'a, T> = Result<&'a mut T>`:**
  - A specific type alias for a mutable reference within a `Result`.

- **`ResultOpt<T> = Result<Option<T>>`:**
  - A specific type alias for a `Result` with an `Option` type.

- **`ResultRef<'a, T> = Result<&'a T>`:**
  - A specific type alias for a reference within a `Result`.

- **`ResultVec<T> = Result<Vec<T>>`:**
  - A specific type alias for a `Result` with a `Vec` type.

- **`Status = Result<()>`:**
  - A specific type alias for a `Result` with an empty tuple, representing success or failure without any additional information.

### Summary

The `ExceptionType` enum defines methods for checking and retrieving information about the type of exception. The `Exception` struct represents an exception instance with various details, and the macros (`exception!`, `err!`, `custom_err!`) provide convenient ways to create and handle exceptions. The result types simplify working with different types of results. Overall, these entities collectively create a comprehensive and modular exception handling system in Rust.
