# Info-201-final
ui <- fluidPage(
  titlePanel("Mario Kart Analysis"),
  sidebarLayout(
    sidebarPanel(
      h2("Control Panel"),
      selectInput(
        inputId = "char_name",
        label = "Select a character",
        #choices = list("Mario", "Luigi", "Browser")
        choices = char_df$Character
      )
    ),
    mainPanel(
      tabsetPanel(
        tabPanel("Plot", plotOutput(outputId = "radar")),
        tabPabel("Table", tableOutput(outputId = "table"))
      )
    )
  ),
    tableOutput(outputId = "table"),
    plotOutput(outputId = "radar")
      
    ),
    
    h1("THIS IS NOT IN THE SIDEBAR LAYOUT"),
    p("IDKDIDIIDIDIDKIDK")
  )
)

server <- function(input, output) {
  #output$testing <- renderText({
    #return(input$char_name)
  #})
  
  make_radar_table <- function(name) {
    data_pt <- filter(char_df, Character == input$char_name)
    data_pt <- select(data_pt, -c(Character, Class))
    
    max_pt <- summarise_all(char_df, max)
    max_pt <- select(max_pt, -c(Character, Class))
    
    min_pt <- summarise_all(char_df, min)
    min_pt <- select(min_pt, -c(Character, Class))
    
    do.call("rbind", list(max_pt, min_pt, data_pt))
  }
  
   output$table <- renderTable ({
  # return(char_df)
  # get the row corresponding to "Mario"
    
    return(make_radar_table(input$char_name))
    
   # return(max_pt)
    output$radar <- renderPlot({
      tb <- make_radar_tb(input$char_df)
      radarchart(tb)
    })
  
  })
