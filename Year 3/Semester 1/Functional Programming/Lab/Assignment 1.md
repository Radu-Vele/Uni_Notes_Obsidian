# Problem Description

> [!info] About 🌥
> - weather app: show data for current location on a chart + daily high and low + total precipitation
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
	- [x] Done

### 2. complete View.Day.view
- add items
	- [x] Done
	
>[!question]
>Is it graded?
- add class
	- [x] Done

### 3. complete View.Week.view
- display the days 
- [x] Done
- Display as h2 first and lat
- [x] Done

### 4. Complete Main according to the comments
- chart data
- [x] Done
- weekly Data
Input: weather -> weather API
Output: weekly Data -> contains a list of daily data for 7 days
- [x] Done

### 5. Implement Model.WeatherData 

- decode hourly data
- [x] Done

- decode weather data
- [x] Done

- to hourly dp
- [x] Done

### 6. Complete Model.WeatherItems and View.WeatherItems

- edit what is displayed on the chart

- Model.WeatherItems 
	- represent the selected categories
	- implement allSelected/isItemSelected
	- implement set
- [x] Done
- View.WeatherItems
	- view with 4 checkboxes using checkbox functions
- Main
	- add the selection logic in update
	- add the checkboxes to view

## Additional requirements
- include lambda
- [x] Done
- pipelines and composition
- [x] Done
- built-in functions
- [x] Done


### Bugs
> [!info] Some issues:
> - the Min value showing on the top of the html page

# App structure figure out


### `Main.elm` file
- is the entry point
- `init` function $\to$ populate a Browser.element record:
	- specify ProdMode & generate the start state and send the command `GotTime` 
	- specify the view, update and subscriptions functions
- `view` function - ensembles the views declared in View.*
- `update` function - processes messages from Runtime to yield new models and commands (like perform a request to get weather)
```elm
-- request to get data
getWeather apiUrl = 
    let
        queryParams =
            List.concat
                [ [ UrlBuilder.string "latitude" <| String.fromFloat 46.77
                  , UrlBuilder.string "longitude" <| String.fromFloat 23.6
                  , UrlBuilder.string "timezone" "auto"
                  , UrlBuilder.string "timeformat" "unixtime"
                  ]
                , List.map (UrlBuilder.string "hourly")
                    [ "temperature_2m"
                    , "precipitation"
                    ]
                ]
    in
    Http.get
        { url = UrlBuilder.crossOrigin apiUrl [ "v1", "forecast" ] queryParams
        , expect = Http.expectJson GotWeather WeatherData.decodeWeatherData
        }
```
- usually no command is issued, only when we go from GotTime to GotWeather


## Model `= {Config, AppState}`
- eventually the state of the app 
```elm
type alias Config =
    { apiUrl : String
    , mode : Mode
    }
    
type AppState
    = WaitingForTime -- initial state
    | HaveTime { time : Time.Posix } -- intermediary state
    | HaveWeatherAndTime Weather -- got data from the API
    | FailedToLoad -- failure
```


## View `: Model -> Html Msg`
- generate an HTML page based on the current model
- defined in multiple files: `main`, `View.Day`, `View.Week`, `View.WeatherItems`, `View.WeatherChart`
- each smaller view function has different parameters that are extracted from the model in the state: `HaveWeatherAndTime Weather` with:
```elm
type alias Weather =
    { time : Time.Posix
    , weather : ApiWeatherData
    , hovering : Hovering
    , selectedItems : SelectedWeatherItems
    }
```


## Update `: Msg -> Model -> Model`
- take a message (Msg) from the elm runtime, the current model and return a new model

```elm
type Msg
    = GotTime Time.Posix
    | GetWeather
    | GotWeather (Result Http.Error ApiWeatherData)
    | OnHover (List (CI.One HourlyDataPoint CI.Dot))
    | ChangeWeatherItemSelection WeatherItem Bool
```

- in our case once we get the weather from the api we keep on modifying fields in the `Model.HaveWeatherAndTime` if we hiver on the chart or check/uncheck boxes.