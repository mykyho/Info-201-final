# Info-201-final

library(dplyr)
library(shiny)
library(plotly)

#import file
child_race_pov <- read.csv("child_race_pov.csv")
child_poverty <- read.csv("Children in poverty.csv")
#food_insecure_18to24 <- read.csv("Adults ages 18 to 24 with food insecurity .csv")

#data cleaning for file 1
child_race_pov <- subset(child_race_pov, DataFormat == "Number")
child_race_pov <- subset(child_race_pov, !(Data %in% c("S", "N.A.")))
child_race_pov <- subset(child_race_pov, !(Race %in% c("Total")))
child_race_pov <- subset(child_race_pov, select = -c(DataFormat, LocationType))

#Data cleaning for file 2
#food_insecure_18to24 <- subset(food_insecure_18to24, select = -c(DataFormat, LocationType))
child_poverty <- subset(child_poverty, DataFormat == "Number")
child_poverty <- subset(child_poverty, select = -c(DataFormat, LocationType))
child_poverty <- subset(child_poverty, !(Data %in% c("S", "N.A.")))

new_set <- child_poverty$TimeFrame >= 2018 & child_poverty$TimeFrame <= 2022
new_set_two <- child_race_pov$TimeFrame >= 2018 & child_race_pov$TimeFrame <= 2022
filtered_df_one <- child_poverty[new_set, ]
filtered_df_two <- child_race_pov[new_set_two, ]


# merged by both location column
both_df <- merge(filtered_df_one, filtered_df_two, by = c("Location", "TimeFrame", "Data"), all = TRUE)

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
                      h3("Key Findings"),
                      p("We discovered that child poverty youth rates have decreased over the past ten years throughout the United States. Although it's been decreasing, the progress has been slow, emphasizing the need for continued efforts and initiatives to further decrease this significant social challenge."),
                      p(a(href = "https://datacenter.aecf.org/data/tables/43-children-in-poverty?loc=1&loct=2#detailed/2/2-53/false/1095/any/322", "Child Poverty Statistics in the U.S.")),
                      p(a(href = "https://datacenter.aecf.org/data/tables/10931-adults-ages-18-to-24-who-sometimes-or-often-did-not-have-enough-food-to-eat-in-the-past-week?loc=1&loct=1#detailed/1/any/false/2501,2485,2475,2470,2460,2461,2421,2420,2102,2101/any/21240", "Food insecurity among adults ages 18 to 24"))
                  ),
                  fluidRow(
                    column(12,
                           tags$img(src = "https://www.hope4youthmn.org/wp-content/uploads/2023/05/services-1-1030x1030.png", 
                                    height = 150, 
                                    width = "30%", 
                                    style = "display: block; margin-left: auto; margin-right: auto;")
                    )
                  )
           )
  ),
  # Poverty by year
  tabPanel("Data Selection",
           sidebarLayout(
             sidebarPanel(
               div(
                 style = "background-color: whitesmoke; padding: 10px; border-radius: 5px; color: black; text-align: left; margin-top: 10px;",
                 p("This scatter plot illustrates childern in poverty. Hover your mouse over the scatter plot to see how many childern each year are in poverty by each state."),
                 p(style = "font-style: italic")
               )
             ),
             mainPanel(
               plotlyOutput("scatterPlotData")
             )
           )
  ),
  # Poverty by state
  tabPanel("Race",
           sidebarLayout(
             sidebarPanel(
               selectInput("raceFilter", "Select", choices = c(both_df$Race)),
               div(
                 style = "background-color: whitesmoke; padding: 10px; border-radius: 5px; color: grey; text-align: left; margin-top: 10px;",
                 p("This scatterplot illustrates ."),
                 p(style = "font-style: italic;")
               )
             ),
             mainPanel(
               plotlyOutput("scatterPlotRace")
             )
           )
  ),
  
  tabPanel("Poverty",
           sidebarLayout(
             sidebarPanel(
               selectInput(
                 inputId = "state_selection",
                 label = "choose state to display",
                 choices = c("All", unique(both_df$Location)),
                 selected = "all"
               )
               
             ),
             mainPanel(
               plotOutput("poverty_chart")
             )
           )
  ),
  
  tabPanel("Analysis",
           p(strong("Title:Child and Young Adult Poverty")),
           p(strong("Authors:Arsima Sisay (asisay@uw.edu), Myky Ho (mho02@uw.edu), Anisha Bains (abains2@uw.edu)")),
           p(strong("Affliation: INFO-201: Technical Foundations of Informatics - The Information School - University of Washington")),
           p(strong("Date: Fall 2023")),
           h3("Keywords"),
           p("Children, Young Adults, Poverty, Rates, Food Insecurity, United States"),
           h3("Abstract"),
           p("Our website ultimately aims to provide insight about whether child and adult youth poverty in the United States has changed throughout years. Our data presents information from the years of 2012 to 2022, with emphasis on raising awareness about the necessary ways to improve this problem. The question we focused on answering throughout our project was how much has poverty changed over the course of 10 years. To help answer our research question, we will analyze datasets regarding child poverty, as well as poverty and food insecurity issues amongst young adults of age from 18-24. By reducing poverty for a large amount of individuals would help improve many issues such as food insecurity, quality of health, and overall quality of life"),
           h3("Design"),
           p("Our project is designed in a way that presents a clear indication about the topics we will be covering throughout our website. The about page, contains information about the importance of our topic and how there are many ways the issues of poverty and food insecurity can be addressed. The about page states our focus about how to further explain the issues, as well as provide helpful information and resources that could potentially positively impact individuals dealing with said issues. Further into our research, we wanted to create three interactive pages showing the rates in which child poverty and food insecurity has made an impact on people throughout the United states. We hoped to create graphs and informative data that could be well considered when identifying the ways in which these issues can be resolved."),
           h3("Purpose"),
           p("We believe that life experiences, especially at a young age, shapes the upbringing of a person. This ignited our desire to ensure that individuals unable to access resources for everyday living are brought into light. Our goal is to not only raise awareness for people but also create a community of students, teachers, friends and family that can lift each other up in times of need. We hope that with the data provided on our site we can educate people about the real numbers of youths not receiving the help that they need. Advocating and spreading awareness of this issue is crucial."),
           h3("Conclusion"),
           p("During the process of completion of our project we learned about the many ways in which people are highly affected by poverty in the United States. Factors such as food insecurity, homelessness, and lack of education contribute to the well known issue of poverty. These consequences play a negative role on individuals, communities, and societies. Raising awareness about poverty will hopefully result in a more equitable world and drive the need to change these factors for people. After researching children and young adults, it was refreshing to see the data of people living in poverty decrease over the years, although it is still an ongoing issue that will optimistically continue to decline.")
  )
)
# Server Logic
server <- function(input, output) {
  filtered_data <- reactive({
    subset(both_df, Location == input$state & TimeFrame == input$time)
  })
  output$scatterPlotData <- renderPlotly({
    plot_data <- filtered_data()
    plot_ly(data = both_df, x = ~Data, y = ~TimeFrame, type = "scatter", mode = "markers", text = ~Location)
  })
  
  #2
  interactive_page <- tabPanel(
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
      p("This chart attempts to show the data in which poverty rates are represented 
      throughout different states in the United States. The box plots 
      presents the spread of the data (percentage of poverty) across each 
      of the 3 categories: high, low, and medium. The ability to select which category 
      to display with the widget adds for further focus.")
    ) 
  )
)
       
  
  race_data <- reactive ({
    subset(both_df, Race == input$raceFilter & Location == "United States")
  })
  output$scatterPlotRace <- renderPlotly({
    plot_ly(data = race_data(), x = ~TimeFrame, y = ~Data, type = "scatter", mode = "markers+lines", text = ~Location)
  })
  
  #3
  filtered_data <- reactive({
    if (input$state_selection == "All") {
      return(both_df)
    } else {
      return(subset(both_df, Location == input$state_selection))
    }
  })
  
  output$poverty_chart <- renderPlot({
    ggplot(filtered_data(), aes(x = Year, y = Rate, fill = State)) +
      geom_bar(stat = "identity", position = "dodge") +
      labs(title = "Poverty Youth Rate Comparison",
           x = "Year",
           y = "Poverty Youth Rate Percentage") +
      theme_minimal()
  })
  output$analysisText <- renderText({
    paste("Additional analysis based on the selected year:", input$yearFilter)
  })
}
# Run the application 
shinyApp(ui, server)
