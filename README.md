# Info-201-final

library(shiny)
library(plotly)

ui <- navbarPage(
  title = "Poverty in Youth",
  tags$head(
    tags$style(HTML("
            body { 
                background-color: #b8bccc;
                font-family: 'cursive', 'Calibri'; 
            }
            h3 { 
                color: Black;
            }
        "))
  ),
  # Home tab
  tabPanel("About",
             column(12, style = "padding-right: 100px;", 
                    #h1("Welcome to Sippin' and Spending!"),
                    div(style = "font-size: 16px;",
                        h3("Project Overview"),
                        p("The advice that many of us have heard is along the lines of, “Life is never a smooth journey, there will always be hurdles along the way.” 
                          As we agree with this statement, we also know that some people have more hurdles than others. 
                          Imagine a world where every young person, regardless of their circumstances, has easy access to resources and support."),
                     br(),
                       h3("Vision"),
                       p("Our vision is to create a world where every young person, regardless of their circumstances, has easy access to vital resources and unwavering support. 
                         We envision a digital platform that serves as a lifeline for youth and young adults seeking assistance with fundamental needs such as shelter, food, and more."),
                      br(), 
                      h3("Problem Statement"),
                        p("Navigating the wealth of information available can be overwhelming, leading many to struggle in finding the help they urgently need. 
                        While support exists, it is often inefficient and unreliable, particularly for young individuals facing adversities. 
                        Research indicates that children living in poverty spend more time surviving than exploring the world around them, leaving them without the crucial assistance they require."),
                        #h3("Key Findings"),
                        #p("We uncovered that developed countries with higher spending amounts have a larger average alcohol consumption as well as lower life expectancies than developing countries. To visualize these trends, please go through                             each webpage for interactive displays of this data!"),
                        #p(a(href = "https://www.who.int/health-topics/alcohol#tab=tab_1", "Learn more about alcohol consumption on the WHO Alcohol Webpage", target = "_blank"))
                    )
             )
           ),
  
server <- function(input, output){
  
}

shinyApp(ui = ui, server = server)
