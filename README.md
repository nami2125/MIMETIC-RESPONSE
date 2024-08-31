# MIMETIC-RESPONSE
MIMETIC ASSIGNMENT 
# Load necessary libraries
library(shiny)

# Define UI for the application
ui <- fluidPage(
  
  # Application title
  titlePanel("Mimetic Response to 'Faith' by Robert Kendall"),
  
  # CSS for basic styling and motion (animated color change)
  tags$style(HTML("
    @keyframes textChange {
      0% {color: red;}
      50% {color: blue;}
      100% {color: green;}
    }
    .animated-text {
      animation: textChange 5s infinite;
      font-size: 24px;
    }
    .sound-button {
      background-color: #f0f0f0;
      border: none;
      padding: 10px 20px;
      font-size: 18px;
    }
  ")),
  
  # Text Output area
  fluidRow(
    column(12,
           div(class="animated-text",
               p("Words shifting, emotions changing, like a wave of colors")
           )
    )
  ),
  
  # Sound Section
  fluidRow(
    column(12,
           tags$audio(src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3", type="audio/mp3", autoplay=NA, controls=NA),
           p("Listen to the changing tone, as it mimics the changing color of the text.")
    )
  ),
  
  # Interactive button to simulate user interaction
  fluidRow(
    column(12,
           actionButton("btnChange", "Click Me!", class="sound-button"),
           textOutput("changeText")
    )
  )
)

# Define server logic for the animation and interaction
server <- function(input, output) {
  
  # Reactive value for changing text on button click
  text_reactive <- reactiveVal("Waiting for change...")
  
  # Observe button click and update text
  observeEvent(input$btnChange, {
    text_reactive("The words shift and change, just as time does.")
  })
  
  # Output the updated text
  output$changeText <- renderText({
    text_reactive()
  })
}

# Run the application 
shinyApp(ui = ui, server = server)
