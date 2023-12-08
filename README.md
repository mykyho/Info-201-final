# Info-201-final
ui <- fluidPage (
  titlePanel("About this project"),
  p("The advice that many of us have heard is along the lines of, “Life is never a smooth journey, there will always be hurdles along the way.” As we agree with this statement, we also know that some people have more hurdles than others.
  Imagine a world where every young person, regardless of their circumstances, has easy access to resources and support. Our project aims to bring this vision to life by bridging the gap between digital resources and the youth and young adults    in need of assistance such as shelter, food and others. "),
  br(),
  titlePanel("Page Describtion"),
  p("here is page description"),
  tags$style(HTML("
      h2 {
            background-color: Teal;
            color: White;
      }")),
)
server <- function(input, output){
  
}

shinyApp(ui = ui, server = server)
