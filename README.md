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
                        h3("Vision"),
                        p("Our vision is to create a world where every young person, regardless of their circumstances, has easy access to vital resources and unwavering support. 
                         We envision a digital platform that serves as a lifeline for youth and young adults seeking assistance with fundamental needs such as shelter, food, and more."),
                        h3("Problem Statement"),
                        p("Navigating the wealth of information available can be overwhelming, leading many to struggle in finding the help they urgently need. 
                        While support exists, it is often inefficient and unreliable, particularly for young individuals facing adversities. 
                        Research indicates that children living in poverty spend more time surviving than exploring the world around them, leaving them without the crucial assistance they require."),
                        #h3("Key Findings"),
                        #p("We uncovered that developed countries with higher spending amounts have a larger average alcohol consumption as well as lower life expectancies than developing countries. To visualize these trends, please go through                             each webpage for interactive displays of this data!"),
                        #p(a(href = "https://youth.gov/youth-topics/runaway-and-homeless-youth/resources-young-parents-children?field_yhp_topic_tid%5B%5D=469&field_yhp_audience_tid=All&field_yhp_type_of_resource_tid=All&=Apply", "Additional                                 resources for youth"))
                        h3("Key Findings"),
                        p("We discovered that child poverty youth rates have decreased over the past ten years throughout the United States. Although it's been decreasing, the progress has been slow, emphasizing the need for continued efforts                           and initiatives to further decrease this significant social challenge."),
                        p(a(href = "https://datacenter.aecf.org/data/tables/43-children-in-poverty?loc=1&loct=2#detailed/2/2-53/false/1095/any/322", "Child Poverty Statistics in the U.S.")),
                        p(a(href = "https://datacenter.aecf.org/data/tables/10931-adults-ages-18-to-24-who-sometimes-or-often-did-not-have-enough-food-to-eat-in-the-past-week?                 loc=1&loct=1#detailed/1/any/false/2501,2485,2475,2470,2460,2461,2421,2420,2102,2101/any/21240", "Food insecurity among adults ages 18 to 24"))
                    ),
                    fluidRow(
                      column(12,
                             tags$img(src = "https://www.hope4youthmn.org/wp-content/uploads/2023/05/services-1-1030x1030.png", 
                                      height = 150, 
                                      width = "30%", 
                                      style = "display: block; margin-left: auto; margin-right: auto;")
                      ),
             )
           ),
  ),
             interactive_page_three <- tabPanel(
  "Poverty",
  titlePanel('Comparing Poverty Youth Rate Percentages of Various States'),
  sidebarLayout(
    sidebarPanel(
      selectInput(
        inputId = "State",
        label = "Choose State to Display",
        choices = list("High" = "High", 
                       "Medium" = "Medium",
                       "Low" = "Low",
                       "All" = "All")
      ), 
    ),
    mainPanel(
      plotlyOutput("Poverty"),
      h2("Description"),
      p("This chart attempts to show the data in which crime rates are represented 
      throughout different states in the United States. The box plots 
      presents the spread of the data (percentage of poverty) across each 
      of the 3 categories: high, low, and medium. The ability to select which category 
      to display with the widget adds for further focus.")
    ) 
  )
)
             
             )
           ),
  
server <- function(input, output){
  
}

shinyApp(ui = ui, server = server)
