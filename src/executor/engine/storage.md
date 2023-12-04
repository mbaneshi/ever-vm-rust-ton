**Description:**

This Rust code appears to be part of a virtual machine implementation, possibly for executing some kind of bytecode or microcode. It includes utility functions and structures related to the management of continuations, stacks, and swapping operations.

**Symbols:**

1. **Enums and Constants:**
   - `Exception`: Enum representing different types of exceptions.
   - `Result`, `ResultMut`, `ResultRef`: Type aliases for `ton_types::Result` with different mutability and ownership.

2. **Structs:**
   - `Gas`: Represents gas state.

3. **Functions:**
   - `continuation_by_address(engine: &mut Engine, address: u16) -> ResultRef<ContinuationData>`: Retrieves a continuation based on its address.
   - `continuation_mut_by_address!(engine:ident, address:expr)`: Macro that returns a mutable reference to a continuation based on its address.
   - `move_stack_from_cc(engine: &mut Engine, dst: u16, drop: Range<usize>) -> Status`: Moves items from the call stack to another continuation's stack.
   - Various utility functions for manipulating lists, items, and swapping operations.

4. **Macros:**
   - `continuation_mut_by_address!`: Macro for getting a mutable reference to a continuation based on its address.

5. **Structs:**
   - `Info`: Struct representing information about an item, including flags and index.
   - `Info` methods: `item`, `list` - Retrieve item or list based on flags and index.

6. **Functions:**
   - `put_to_list(engine: &mut Engine, x: &mut Info, y: &mut StackItem) -> Result<Option<StackItem>>`: Puts an item into a list.
   - `put_to_list_from_item(engine: &mut Engine, x: &mut Info, y: &Info) -> Result<Option<StackItem>>`: Puts an item into a list from another item.
   - `put_to_list_from_list(engine: &mut Engine, x: &mut Info, y: &mut Info) -> Result<Option<StackItem>>`: Puts an item into a list from another list.
   - `swap_with_list(engine: &mut Engine, x: Info, y: Info) -> Status`: Swaps an item with a list.
   - `swap_between_lists(engine: &mut Engine, x: Info, y: Info) -> Status`: Swaps items between two lists.

**Note:** 
- The code uses the `ton_types` and `log` crates.
- The `address_tag!` and `storage_index!` macros are used to extract information from addresses.
- The code involves manipulating continuations, stacks, and various utility functions for managing items and lists.

***

Certainly, let's delve deeper into each listed entity:

1. **Enums and Constants:**
   - `Exception`: Enum representing different types of exceptions that can occur during the execution of the virtual machine.
   - `Result`, `ResultMut`, `ResultRef`: Type aliases for `ton_types::Result` with different mutability and ownership.

2. **Structs:**
   - `Gas`: Represents gas state. Unfortunately, the definition of `Gas` is not provided in this snippet, so its exact structure and purpose are unclear.

3. **Functions:**

   - `continuation_by_address(engine: &mut Engine, address: u16) -> ResultRef<ContinuationData>`:
     - Given an engine and an address, this function retrieves a reference (`ResultRef`) to a `ContinuationData` associated with that address.
     - `address_tag!` macro extracts information about the address, and based on the tag, it fetches the continuation from the engine.

   - `continuation_mut_by_address!(engine:ident, address:expr)`:
     - Macro that returns a mutable reference to a continuation based on its address.
     - Similar to `continuation_by_address` but allows mutability.

   - `move_stack_from_cc(engine: &mut Engine, dst: u16, drop: Range<usize>) -> Status`:
     - Moves items from the call stack (`engine.cc.stack`) to another continuation's stack.
     - The `dst` parameter represents the destination address, and the `drop` parameter defines a range of items to be dropped from the source stack.
     - Handles various cases such as stack overflow, stack underflow, and manages the transfer of items between stacks.

   - Various utility functions:
     - `put_to_list(engine: &mut Engine, x: &mut Info, y: &mut StackItem) -> Result<Option<StackItem>>`:
       - Puts an item into a list specified by `x`.
       - `x` is an `Info` struct containing information about the list (flags and index), and `y` is the item to be put into the list.

     - `put_to_list_from_item(engine: &mut Engine, x: &mut Info, y: &Info) -> Result<Option<StackItem>>`:
       - Puts an item into a list from another item.
       - Checks for type compatibility before the operation.

     - `put_to_list_from_list(engine: &mut Engine, x: &mut Info, y: &mut Info) -> Result<Option<StackItem>>`:
       - Puts an item into a list from another list.
       - Checks for type compatibility before the operation.

     - `swap_with_list(engine: &mut Engine, x: Info, y: Info) -> Status`:
       - Swaps an item with a list.
       - If the list (`y`) is not null, it puts the item into the list.

     - `swap_between_lists(engine: &mut Engine, x: Info, y: Info) -> Status`:
       - Swaps items between two lists.
       - If the destination list (`y`) has an item at the specified index, it swaps items between the two lists.

4. **Macros:**

   - `continuation_mut_by_address!`:
     - Macro for getting a mutable reference to a continuation based on its address.
     - Similar to `continuation_by_address` but in macro form.

5. **Structs:**

   - `Info`:
     - A struct representing information about an item, including flags and index.
     - Implements methods like `item` and `list` for retrieving items or lists based on the stored information.

6. **Functions:**

   - `Info` methods:
     - `item`: Returns a mutable reference to an item based on the stored flags and index.
     - `list`: Returns a mutable reference to a `SaveList` based on the stored flags and index.

**Note:**
- The code is designed to manipulate and manage continuations, stacks, and various utility functions for managing items and lists.
- The detailed implementation of the `Gas` struct and certain macros like `address_tag!` and `storage_index!` are not provided in this snippet.

 ***


 Certainly, let's delve deeper into each listed entity:

1. **Enums and Constants:**
   - `Exception`: Enum representing different types of exceptions that can occur during the execution of the virtual machine.
   - `Result`, `ResultMut`, `ResultRef`: Type aliases for `ton_types::Result` with different mutability and ownership.

2. **Structs:**
   - `Gas`: Represents gas state. Unfortunately, the definition of `Gas` is not provided in this snippet, so its exact structure and purpose are unclear.

3. **Functions:**

   - `continuation_by_address(engine: &mut Engine, address: u16) -> ResultRef<ContinuationData>`:
     - Given an engine and an address, this function retrieves a reference (`ResultRef`) to a `ContinuationData` associated with that address.
     - `address_tag!` macro extracts information about the address, and based on the tag, it fetches the continuation from the engine.

   - `continuation_mut_by_address!(engine:ident, address:expr)`:
     - Macro that returns a mutable reference to a continuation based on its address.
     - Similar to `continuation_by_address` but allows mutability.

   - `move_stack_from_cc(engine: &mut Engine, dst: u16, drop: Range<usize>) -> Status`:
     - Moves items from the call stack (`engine.cc.stack`) to another continuation's stack.
     - The `dst` parameter represents the destination address, and the `drop` parameter defines a range of items to be dropped from the source stack.
     - Handles various cases such as stack overflow, stack underflow, and manages the transfer of items between stacks.

   - Various utility functions:
     - `put_to_list(engine: &mut Engine, x: &mut Info, y: &mut StackItem) -> Result<Option<StackItem>>`:
       - Puts an item into a list specified by `x`.
       - `x` is an `Info` struct containing information about the list (flags and index), and `y` is the item to be put into the list.

     - `put_to_list_from_item(engine: &mut Engine, x: &mut Info, y: &Info) -> Result<Option<StackItem>>`:
       - Puts an item into a list from another item.
       - Checks for type compatibility before the operation.

     - `put_to_list_from_list(engine: &mut Engine, x: &mut Info, y: &mut Info) -> Result<Option<StackItem>>`:
       - Puts an item into a list from another list.
       - Checks for type compatibility before the operation.

     - `swap_with_list(engine: &mut Engine, x: Info, y: Info) -> Status`:
       - Swaps an item with a list.
       - If the list (`y`) is not null, it puts the item into the list.

     - `swap_between_lists(engine: &mut Engine, x: Info, y: Info) -> Status`:
       - Swaps items between two lists.
       - If the destination list (`y`) has an item at the specified index, it swaps items between the two lists.

4. **Macros:**

   - `continuation_mut_by_address!`:
     - Macro for getting a mutable reference to a continuation based on its address.
     - Similar to `continuation_by_address` but in macro form.

5. **Structs:**

   - `Info`:
     - A struct representing information about an item, including flags and index.
     - Implements methods like `item` and `list` for retrieving items or lists based on the stored information.

6. **Functions:**

   - `Info` methods:
     - `item`: Returns a mutable reference to an item based on the stored flags and index.
     - `list`: Returns a mutable reference to a `SaveList` based on the stored flags and index.

**Note:**
- The code is designed to manipulate and manage continuations, stacks, and various utility functions for managing items and lists.
- The detailed implementation of the `Gas` struct and certain macros like `address_tag!` and `storage_index!` are not provided in this snippet.

***


Certainly, let's go even deeper into the provided code:

### 1. Enums and Constants:

- **`Exception` Enum:**
  - Represents different types of exceptions that can occur during the execution of the virtual machine.
  - The specific exceptions and their meanings are not defined in this snippet, and the actual implementation may be in another part of the codebase.

- **`Result`, `ResultMut`, `ResultRef` Aliases:**
  - These are type aliases for `ton_types::Result` with different mutability and ownership.
  - `Result` might represent a result that can be mutated, `ResultMut` a mutable result, and `ResultRef` a reference to a result.

### 2. Structs:

- **`Gas` Struct:**
  - The definition of the `Gas` struct is not provided in this snippet.
  - It's mentioned as representing gas state, suggesting it might be related to managing computational resources or execution limits.

### 3. Functions:

#### `continuation_by_address(engine: &mut Engine, address: u16) -> ResultRef<ContinuationData>`

- Given an `engine` and an `address`, retrieves a reference to a `ContinuationData` associated with that address.
- Uses the `address_tag!` macro to extract information about the address, and based on the tag, fetches the continuation from the engine.
- Returns a `ResultRef` indicating success or failure.

#### `continuation_mut_by_address!(engine:ident, address:expr)`

- Macro that returns a mutable reference to a continuation based on its address.
- Similar to `continuation_by_address` but allows mutability.

#### `move_stack_from_cc(engine: &mut Engine, dst: u16, drop: Range<usize>) -> Status`

- Moves items from the call stack (`engine.cc.stack`) to another continuation's stack.
- Takes a destination address (`dst`) and a range (`drop`) specifying items to drop from the source stack.
- Handles cases such as stack overflow, stack underflow, and manages the transfer of items between stacks.
- Returns a `Status` indicating success or an error.

#### Various Utility Functions:

- `put_to_list(engine: &mut Engine, x: &mut Info, y: &mut StackItem) -> Result<Option<StackItem>>`:
  - Puts an item (`y`) into a list specified by `x`.
  - `x` is an `Info` struct containing information about the list (flags and index).

- `put_to_list_from_item(engine: &mut Engine, x: &mut Info, y: &Info) -> Result<Option<StackItem>>`:
  - Puts an item into a list from another item.
  - Checks for type compatibility before the operation.

- `put_to_list_from_list(engine: &mut Engine, x: &mut Info, y: &mut Info) -> Result<Option<StackItem>>`:
  - Puts an item into a list from another list.
  - Checks for type compatibility before the operation.

- `swap_with_list(engine: &mut Engine, x: Info, y: Info) -> Status`:
  - Swaps an item with a list.
  - If the list (`y`) is not null, it puts the item into the list.

- `swap_between_lists(engine: &mut Engine, x: Info, y: Info) -> Status`:
  - Swaps items between two lists.
  - If the destination list (`y`) has an item at the specified index, it swaps items between the two lists.

### 4. Macros:

- **`continuation_mut_by_address!` Macro:**
  - A macro for getting a mutable reference to a continuation based on its address.
  - Similar to `continuation_by_address` but in macro form.

### 5. Structs:

- **`Info` Struct:**
  - Represents information about an item, including flags and index.
  - Implements methods like `item` and `list` for retrieving items or lists based on the stored information.

### 6. Functions:

- **`Info` Methods:**
  - `item`: Returns a mutable reference to an item based on the stored flags and index.
  - `list`: Returns a mutable reference to a `SaveList` based on the stored flags and index.

### Additional Notes:

- The code involves detailed manipulation of continuations, stacks, and utility functions for managing items and lists.
- Certain parts of the code, such as the `Gas` struct and the implementation of macros like `address_tag!` and `storage_index!`, are not provided in this snippet.
- The code is designed to handle various aspects of the virtual machine's state, including exceptions and gas management.

***


### 1. `swap` Function:

This function performs a swap operation between two addresses (`x` and `y`). The addressing scheme is described in `executor/microcode.rs`. The function handles different cases based on the types of addresses and tags associated with them.

- **Input:**
  - `engine`: A mutable reference to the virtual machine's `Engine`.
  - `x` and `y`: The addresses to be swapped.

- **Process:**
  - It first ensures that `x` has a lower or equal tag compared to `y`.
  - Constructs `Info` structs for `x` and `y`, containing flags and index information.
  - Matches the tag of `x` and then further matches the tag of `y`.
    - If both are lists (`CC_SAVELIST`, `CTRL`, `CTRL_SAVELIST`, `VAR_SAVELIST`), it calls `swap_between_lists`.
    - If `y` is a variable (`VAR`), it calls `swap_with_list`.
    - Otherwise, it fails with an error message.

- **Output:**
  - Returns a `Status` indicating success or an error.

### 2. Microfunctions:

#### a. `apply_savelist_excluding_c0_c1`

- Applies the savelist of `CC` to control continuations (`CTRL`) excluding the first two indexes (`c[0]` and `c[1]`).
- Removes the first two elements from `CC.savelist`.
- Applies the remaining savelist to control continuations.

#### b. `apply_savelist`

- Applies the savelist of `CC` to control continuations (`CTRL`).
- Does not exclude any indexes.

#### c. `copy_to_var`

- Copies the content of a specified source address (`src`) to a variable in `ctx.cmd`.
- Supports copying from `CC`, `CTRL`, `STACK`, and `VAR`.

#### d. `fetch_reference`

- Fetches a reference from `CC` and pushes it as a variable in `ctx.cmd`.
- Only supports fetching from `CC`.

#### e. `fetch_stack`

- Fetches a specified number of items from the top of `CC` stack and pushes them as variables in `ctx.cmd`.
- Fails with a stack underflow error if the depth is greater than the current stack depth.

#### f. `pop_all`

- Pops all items from `CC` stack and pushes them to the stack specified by the destination address (`dst`).
- The number of items to pop is determined by the `nargs` of the continuation at the destination address.

#### g. `pop_range`

- Pops a specified range of items from `CC` stack and pushes them to the stack specified by the destination address (`dst`).
- The range is determined by the `drop` parameter.
- Handles gas consumption for stack splitting and concatenation.

### Additional Notes:

- The functions and microfunctions operate on the virtual machine's engine, manipulating stacks, continuations, and variables.
- The code uses macros like `address_tag!` and `storage_index!` to extract information from addresses.
- Various error conditions are handled, such as type-check errors and stack underflows.
- Gas consumption is considered for certain operations, suggesting resource management in the virtual machine.



  Certainly, let's provide more detail for each section of the code:

### 1. `swap` Function:

This function is responsible for swapping values between two addresses (`x` and `y`). The function takes into account the addressing scheme described in `executor/microcode.rs`.

- **Input:**
  - `engine`: A mutable reference to the virtual machine's `Engine`.
  - `x` and `y`: The addresses to be swapped.

- **Details:**
  - It starts by ensuring that `x` has a lower or equal tag compared to `y`. If not, it swaps them.
  - Constructs `Info` structs for `x` and `y`, containing flags and index information.
  - It then matches the tag of `x` and further matches the tag of `y`.
    - If both are lists (`CC_SAVELIST`, `CTRL`, `CTRL_SAVELIST`, `VAR_SAVELIST`), it calls `swap_between_lists`.
    - If `y` is a variable (`VAR`), it calls `swap_with_list`.
    - Otherwise, it fails with an error message.

- **Output:**
  - Returns a `Status` indicating success or an error.

### 2. Microfunctions:

#### a. `apply_savelist_excluding_c0_c1`

- **Details:**
  - Removes the first two elements from `CC.savelist`.
  - Applies the remaining savelist to control continuations (`CTRL`).

#### b. `apply_savelist`

- **Details:**
  - Applies the savelist of `CC` to control continuations (`CTRL`).

#### c. `copy_to_var`

- **Details:**
  - Copies the content of a specified source address (`src`) to a variable in `ctx.cmd`.
  - Supports copying from `CC`, `CTRL`, `STACK`, and `VAR`.

#### d. `fetch_reference`

- **Details:**
  - Fetches a reference from `CC` and pushes it as a variable in `ctx.cmd`.
  - Only supports fetching from `CC`.

#### e. `fetch_stack`

- **Details:**
  - Fetches a specified number of items from the top of `CC` stack and pushes them as variables in `ctx.cmd`.
  - Fails with a stack underflow error if the depth is greater than the current stack depth.

#### f. `pop_all`

- **Details:**
  - Pops all items from `CC` stack and pushes them to the stack specified by the destination address (`dst`).
  - The number of items to pop is determined by the `nargs` of the continuation at the destination address.

#### g. `pop_range`

- **Details:**
  - Pops a specified range of items from `CC` stack and pushes them to the stack specified by the destination address (`dst`).
  - The range is determined by the `drop` parameter.
  - Handles gas consumption for stack splitting and concatenation.

### Additional Notes:

- The functions and microfunctions operate on the virtual machine's engine, manipulating stacks, continuations, and variables.
- The code uses macros like `address_tag!` and `storage_index!` to extract information from addresses.
- Various error conditions are handled, such as type-check errors and stack underflows.
- Gas consumption is considered for certain operations, suggesting resource management in the virtual machine.

 ***

 ### 1. `swap` Function:

- **Summary:**
  - Swaps values between two addresses (`x` and `y`) in the virtual machine.
  - Handles different cases based on the types of addresses and their tags.
  - Utilizes macros like `address_tag!` and `storage_index!` for address analysis.
  - Gas consumption considered for specific operations.

### 2. Microfunctions:

#### a. `apply_savelist_excluding_c0_c1` and b. `apply_savelist`

- **Summary:**
  - Apply savelist from `CC` to control continuations (`CTRL`).
  - Excludes the first two elements (`c[0]` and `c[1]`) in the first function.

#### c. `copy_to_var`

- **Summary:**
  - Copies content from specified source address (`src`) to a variable in `ctx.cmd`.
  - Supports copying from `CC`, `CTRL`, `STACK`, and `VAR`.

#### d. `fetch_reference`

- **Summary:**
  - Fetches a reference from `CC` and pushes it as a variable in `ctx.cmd`.
  - Limited to fetching from `CC`.

#### e. `fetch_stack`

- **Summary:**
  - Fetches a specified number of items from the top of `CC` stack and pushes them as variables in `ctx.cmd`.
  - Handles stack underflow errors.

#### f. `pop_all` and g. `pop_range`

- **Summary:**
  - Pop items from `CC` stack and push to a specified stack (determined by `dst`).
  - `pop_range` handles a specified range and considers gas consumption.

### Additional Insights:

- Detailed manipulation of virtual machine state, involving stacks, continuations, and variables.
- Addressing schemes and tag analysis play a crucial role in operations.
- Gas consumption is taken into account for resource management.
- Various error conditions are handled, enhancing code robustness.
