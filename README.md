# daterangepicker

<p align="center">
  <img src="./man/figures/daterangepicker.PNG" align="right" width="300"/>
</p>

<!-- badges: start -->
[![Travis build status](https://travis-ci.org/trafficonese/daterangepicker.svg?branch=master)](https://travis-ci.org/trafficonese/daterangepicker)
[![AppVeyor build status](https://ci.appveyor.com/api/projects/status/github/trafficonese/daterangepicker?branch=master&svg=true)](https://ci.appveyor.com/project/trafficonese/daterangepicker)
[![Lifecycle: maturing](https://img.shields.io/badge/lifecycle-maturing-blue.svg)](https://www.tidyverse.org/lifecycle/#maturing)
[![Codecov test coverage](https://codecov.io/gh/trafficonese/daterangepicker/branch/master/graph/badge.svg)](https://codecov.io/gh/trafficonese/daterangepicker?branch=master)
<!-- badges: end -->

Custom Shiny input binding for a [Date Range Picker](https://www.daterangepicker.com/).

## Installation

``` r
# install.packages("remotes")
remotes::install_github("trafficones/daterangepicker")
```

## Example

A basic example of a Date Range Picker:

``` r
library(shiny)
library(daterangepicker)

## UI ##########################
ui <- fluidPage(
  daterangepicker(
    inputId = "daterange",
    label = "Pick a Date",
    start = Sys.Date() - 30, end = Sys.Date(),
    style = "width:100%; border-radius:4px",
    icon = icon("calendar")
  ),
  verbatimTextOutput("print"),
  actionButton("act", "Update Daterangepicker"),
)

## SERVER ##########################
server <- function(input, output, session) {
  output$print <- renderPrint({
    req(input$daterange)
    input$daterange
  })
  observeEvent(input$act, {
    updateDaterangepicker(session, "daterange",
                          start = Sys.Date(), 
                          end = Sys.Date() - 100)
  })
}

shinyApp(ui, server)
```

Further examples are in [/inst/examples/](https://github.com/trafficonese/daterangepicker/tree/master/inst/examples)

## Further Information

Check out the [Configuration Generator](https://www.daterangepicker.com/#config) for a Live-Demo of the different options. 
