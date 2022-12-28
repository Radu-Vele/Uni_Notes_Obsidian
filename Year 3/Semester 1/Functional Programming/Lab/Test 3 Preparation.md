# Haskell Test 1

> [!info] Goals:
> - practice with haskell syntax and concepts
> - exercise
> - understand given concepts

## L8 Haskell Introduction
- syntax
- basic exercises

### Concepts:
- type definitions + aliases `data <constructor> = <sum/product type>` 
	- records 
- guards for pattern matching
	- must be exhaustive, but compiles anyway
- `@` pattern bindings
- list comprehensions
	- ranges

- Syntax sugaring:
	- infix operators `infixl <precedence> <operator>`
		- [x] Visited
	- infix function call
		- [x] Visited
	- sections - can use the operator as a function partially applied
	- composition: `$` = function application and `.` = left compose (maintain order of function application)

## L9 Type Classes
- types vs kinds
- class hierarchy + type classes

### Concepts:
- **Kinds** = `how many other types does it take to define the type?`
	- `*` generic | or `* -> *` non generic
- Generic code - use contraints a.k.a. types that a variable can be (such that we can perform some operation with it) a.k.a. ***Type Classes***
- Type classes
	- may find similarities in Java interfaces
- How to implement instances
```haskell
data Color = R | G | B

instance Show Color where
	show --any possibility of type Color -- = ...
```
- .
	- can be derived by compiler
- define class
```haskell
class YesNo a where
	yesno :: a -> Bool
```
-  examples:
	- Monoid
		- `<>` op
	- Semigroup
		- `mempty` op
	- can extend these concepts for natural numbers wrapped in Sum and Product types

> [!question] Questions
> - Re-read `Kind` concept

## L10 Monads and IO
- functors, applicatives, monads = other type classes
- I/O  programs

### Concepts:
- **functor** - supports `fmap` function a.k.a. `<$>` infix form
```haskell
-- usage
function <$> valueInContext -- output: result in context
```
- examples of functors: Maybe, List

-  **Applicative** - support `<*>` operator or `pure`
- extend functor concept + Apply a function wrapped in a context to a value wrapped in a context - can chain functions in contexts
- sugaring: **`liftA2`**, **`liftA3`** - shorter pass them as argument the function and arguments
	- **`sequenceA`** generalize lift to invert the structure of the list and the applicative inside

- **Monad** - support `>>=` (unpack nested structures that are the result of map operations)  function and `return` (like pure)
	- good for chaining operation that can fail