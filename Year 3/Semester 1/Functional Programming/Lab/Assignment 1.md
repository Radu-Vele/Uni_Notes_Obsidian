# Problem Description

> [!info] About 🌥
> - weather app: show data for current location on a charp + daily high and low + total precipitation
> - data is retrieved from a server

## Remarks
- styling is not the key
- don't take complex user input

## Resource code
### `Main.elm`
- most of it is implemented
- skeleton for app
- definitions of `Msg`,  `Update`, `View`, getting information from the API

### `Model.elm`
- data definition
- state of the app

### Stages
- understand given code (`Main.elm`, `Model.elm`)
- run tests
- make sure the views work
- implement project tasks

---

# Project Tasks ☑

### 1. implement functions in Utils module
- `maybeToList`
	- [x] Done
-  `minimumBy` and `maximumBy`
	- [x] Done

> [!question] Questions
> Can I use the List functions?

- `zipFilter`
	- [x] Done
- `groupBy`
	- [x] Done

- Figure out how to Test
	- [ ] Done

### 2. complete View.Day.view

- add items
	- [ ] Done
- add class
	- [ ] Done

### 3. complete View.Week.view
### 4. Complete Main according to the comments
### 5. Implement Model.WeatherData 
### 6. Complete Model.WeatherItems and View.WeatherItems

## Additional requirements
- include lambda
- pipelines and composition
- built-in functions