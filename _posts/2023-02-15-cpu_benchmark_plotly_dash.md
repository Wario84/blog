---

layout: post
title: "Creating a Dashboard of CPU Benchmarks Using R and Python."
author: "Mario H. Gonzalez-Sauri"
date: "2023-02-15"
keywords: sample1, sample2, sample3
---


## Introduction

In this post I will teach you how to create and deploy a dashboard with
a preview of the dataset alongside useful data visualization tools.
Dashboards are useful for creating interactive and customizable data
visualizations and web applications. They allow you to create a dynamic
user interface that can interact with data and update in real-time,
making it an excellent tool for data exploration, analysis, and sharing.
Dashboards can be used for a wide range of purposes, from monitoring
business metrics to visualizing scientific data.

To create the dashboard, I will combine R an Python to take advantage of
strengths of each language for web scraping, data cleaning, dashboard
creation and deployment. My source to gather CPU information and
benchmarks is <a href="https://www.cpubenchmark.net/cpu_list.php">CPU
list from cpubenchmark.net</a>. The goal is to scrap this data to create
a dataset of benchmarks for our CPU dashboard example.

## Web Scrapping HTML tables with rvest

The library `rvest` from R has many interesting functions for web
scrapping. We are interested a function that can transform a HTML tables
(`<table>` and `</table>`) into readable dataframes.

``` r
library("rvest")

## Read data
webpage <- read_html("https://www.cpubenchmark.net/cpu_list.php")
tbls <- webpage %>%
  html_nodes("table") %>%
  html_table(fill = TRUE)
length(tbls)
```

    ## [1] 3

``` r
head(tbls[[2]])
```

    ## # A tibble: 6 × 5
    ##   `CPU Name`              `CPU Mark(higher is better)` Rank(lo…¹ CPU V…² Price…³
    ##   <chr>                   <chr>                            <int>   <dbl> <chr>  
    ## 1 AArch64 rev 2 (aarch64) 2,246                             2187      NA <NA>   
    ## 2 AArch64 rev 4 (aarch64) 1,797                             2439      NA <NA>   
    ## 3 AC8257V/WAB             774                               3269      NA <NA>   
    ## 4 AMD 3015Ce              2,088                             2263      NA <NA>   
    ## 5 AMD 3015e               2,691                             1969      NA <NA>   
    ## 6 AMD 3020e               2,446                             2069      NA <NA>   
    ## # … with abbreviated variable names ¹​`Rank(lower is better)`,
    ## #   ²​`CPU Value(higher is better)`, ³​`Price(USD)`

Now the next step is to convert this table into a dataframe and perform
some basic data cleaning. We are going to use regular expressions to
transform strings of character into numeric and integer values.

``` r
cpus_bench <- tbls[[2]]
cpus_bench$`CPU Mark(higher is better)` <- as.numeric(gsub(",", "", cpus_bench$`CPU Mark(higher is better)`))
cpus_bench$`Rank(lower is better)` <- as.numeric(cpus_bench$`Rank(lower is better)`)
cpus_bench$`CPU Value(higher is better)` <- as.numeric(cpus_bench$`CPU Value(higher is better)`)
cpus_bench$`Price(USD)` <-  gsub("(^\\$)|(\\*$)", "", cpus_bench$`Price(USD)`)
cpus_bench$`Price(USD)` <-  gsub(",", "", cpus_bench$`Price(USD)`)
cpus_bench$`Price(USD)` <- as.numeric(cpus_bench$`Price(USD)`)
head(cpus_bench)
```

    ## # A tibble: 6 × 5
    ##   `CPU Name`              `CPU Mark(higher is better)` Rank(lo…¹ CPU V…² Price…³
    ##   <chr>                                          <dbl>     <dbl>   <dbl>   <dbl>
    ## 1 AArch64 rev 2 (aarch64)                         2246      2187      NA      NA
    ## 2 AArch64 rev 4 (aarch64)                         1797      2439      NA      NA
    ## 3 AC8257V/WAB                                      774      3269      NA      NA
    ## 4 AMD 3015Ce                                      2088      2263      NA      NA
    ## 5 AMD 3015e                                       2691      1969      NA      NA
    ## 6 AMD 3020e                                       2446      2069      NA      NA
    ## # … with abbreviated variable names ¹​`Rank(lower is better)`,
    ## #   ²​`CPU Value(higher is better)`, ³​`Price(USD)`

Now that we have the data in good shape, it is time to retrieve more
information on CPU benchmarks. The `cpus_bench` contains information on
4080 CPUs, however, to make the bashboard more efective, I want to
concentrate on the top-1000 CPUs according to the CPU Mark.

``` r
## Sort according to CPU Mark
cpus_bench <- cpus_bench[order(cpus_bench$`CPU Mark(higher is better)`, decreasing = T), ]
cpus_bench_1000 <- cpus_bench[1:1000,]
head(cpus_bench_1000, 10L)
```

    ## # A tibble: 10 × 5
    ##    `CPU Name`                        CPU Mark(higher i…¹ Rank(…² CPU V…³ Price…⁴
    ##    <chr>                                           <dbl>   <dbl>   <dbl>   <dbl>
    ##  1 AMD EPYC 9654                                  124119       1    10.5  11805 
    ##  2 AMD Ryzen Threadripper PRO 5995WX               96237       2    14.5   6645.
    ##  3 AMD EPYC 7773X                                  90731       3    21.4   4249 
    ##  4 AMD EPYC 7763                                   85944       4    23.4   3665 
    ##  5 AMD EPYC 7J13                                   85661       5    NA       NA 
    ##  6 AMD EPYC 7713                                   85521       6    23.1   3700.
    ##  7 AMD EPYC 7713P                                  83439       7    18.3   4550 
    ##  8 AMD Ryzen Threadripper PRO 3995WX               83097       8    13.3   6267.
    ##  9 AMD EPYC 7V13                                   82878       9    NA       NA 
    ## 10 AMD Ryzen Threadripper 3990X                    81109      10    11.5   7069 
    ## # … with abbreviated variable names ¹​`CPU Mark(higher is better)`,
    ## #   ²​`Rank(lower is better)`, ³​`CPU Value(higher is better)`, ⁴​`Price(USD)`

Very interesting, in the top-10 we find only AMD processors…

To add the rest of the CPU benchmark we are going to take advantage of
this simple function that takes the name of a CPU and creates an HTML
link that will be used by a web scrapping algorithm to retrieve the CPU
benchmarks.

``` r
i <- 1L
paste0("https://www.cpubenchmark.net/cpu.php?cpu=", gsub(" ", "\\+", cpus_bench_1000$`CPU Name`[i]))
```

    ## [1] "https://www.cpubenchmark.net/cpu.php?cpu=AMD+EPYC+9654"

The idea is to write a simple loop that would iterate over all the
top-1000 CPUs and gather information on benchmarks, such as
“integer_math(MOps/Sec)”,“floating_point_math(MOps/Sec)”,“find_prime_numbers(Million
Primes/Sec)”, ect…

``` r
# read in HTML data
i <- 1L
df_bind <- list()
for(i in 1L:1000L){
webpage <- read_html(paste0("https://www.cpubenchmark.net/cpu.php?cpu=", gsub(" ", "\\+", cpus_bench_1000$`CPU Name`[i])))
tbls <- webpage %>%
  html_nodes("table") %>%
  html_table(fill = TRUE)
df <- try(data.table(t(tbls[[2]][2])))
if(any(class(df)%in%"data.table")){
  if(ncol(df) == 9){
    setnames(df, t(tbls[[2]][1]))
    year <- as.integer(sub("^.*\\s", "",trimws(gsub('</p>.*$', '', gsub('^.*<strong class="bg-table-row">CPU First Seen on Charts:</strong>', "", webpage)))))
    gz <- as.integer(sub("\\s.*", "",trimws(gsub('</p>.*$', '', gsub('^.*<strong>Clockspeed:</strong>', "", webpage)))))
    cores <- as.integer(trimws(gsub('<strong>.*$', '', gsub('^.*<strong>Cores:</strong>', "", webpage))))
    threads <- as.integer(trimws(gsub('</p>.*$', '', gsub('^.*<strong>Threads:</strong>', "", webpage))))
    df_bind[[i]] <- cbind.data.frame(cpus_bench_1000[i,], df, gz, cores, threads, year)  
  }
}
}

cpus_bench_full <- rbindlist(df_bind, fill = TRUE)
head(cpus_bench_full)
```

The algorithm may seem a bit intimidating but it is actually quite
simple. It is gathering pieces of information on specific parts of the
HTML code. For instance, to gather the information on the CPU benchmarks
we are always scrapping the second table from the website as
`tbls[[2]][2]`. Then we are scrapping the begging and end of HTML tabs
that contain useful information such as `gz`, `cores` and the `threads`
from the HTML source code. The final data set looks like this:

    ##   X                          cpu_name cpu_mark.higher_is_better.
    ## 1 1                     AMD EPYC 9654                     124119
    ## 2 2 AMD Ryzen Threadripper PRO 5995WX                      95829
    ## 3 3                    AMD EPYC 7773X                      90731
    ## 4 4                     AMD EPYC 7763                      85944
    ## 5 5                     AMD EPYC 7J13                      85661
    ## 6 6                     AMD EPYC 7713                      85521
    ##   cpu_value.higher_is_better. price_usd integer_math.MOps.Sec.
    ## 1                       10.51  11805.00                 978227
    ## 2                       14.98   6399.00                 631867
    ## 3                       21.11   4299.00                 533457
    ## 4                       23.26   3695.00                 547840
    ## 5                          NA        NA                 555507
    ## 6                       23.11   3699.99                 533785
    ##   floating_point_math.MOps.Sec. find_prime_numbers.Million.Primes.Sec.
    ## 1                        522611                                     NA
    ## 2                        343904                                    676
    ## 3                        301129                                     NA
    ## 4                        299973                                    665
    ## 5                        300486                                    686
    ## 6                        272582                                    621
    ##   random_string_sorting.Thousand.Strings.Sec. data_encryption.MBytes.Sec.
    ## 1                                          NA                      187949
    ## 2                                         676                      132563
    ## 3                                          NA                      135770
    ## 4                                         665                      124591
    ## 5                                         686                      123954
    ## 6                                         621                      107100
    ##   data_compression.MBytes.Sec. physics.Frames.Sec.
    ## 1                           NA                  NA
    ## 2                           NA                  NA
    ## 3                           NA                  NA
    ## 4                           NA                  NA
    ## 5                           NA                  NA
    ## 6                           NA                  NA
    ##   extended_instructions.Million.Matrices.Sec. single_thread.MOps.Sec. ghz cores
    ## 1                                      200277                    2893   2    96
    ## 2                                      123388                    3302   2    64
    ## 3                                       91298                    2513   2    64
    ## 4                                       98801                    2576   2    64
    ## 5                                       99971                    2449   2    64
    ## 6                                       94897                    2718   2    64
    ##   threads year
    ## 1     192 2022
    ## 2     128 2022
    ## 3     128 2022
    ## 4     128 2021
    ## 5     128 2021
    ## 6     128 2021

## Dasboard in Plotly Dash from Python

The library that I am going to use to create the dashboard is called
`Plotly Dash`. Plotly Dash has several advantages for deploying a static
web application compared to other libraries. Firstly, it has high level
of interactivity, meaning that users are able to play around with the
data, apply filters, and perform various operations. Secondly, in my
view, it is also flexible as it allows users to create an customize
different plots and layouts, and it is relatively easy to customize.
Thirdly, it has a high level of integration specially with Pandas and
Numpy that are the main libraries that are commonly use of data science
in Python. Finally, the library is relatively easy to deploy at zero
cost as a static website that can be easily embedded or used as a stand
alone service.

Don’t let the code overwhelm you! The structure of the dashboard python
code is simple, we start by loading the packages that we are going to
use. The first line loads the entire Dash library to be used in the
script and the the next three lines import specific modules from the
`Dash` library, which are `dcc`, `html`, and `dash_table`. These modules
are needed to create the visual components of the dashboard such as
tables, dropdowns menus, graphs, and other HTML elements. `Pandas` is
imported in order to read and manipulate the dataset, which is stored in
a CSV file. Then, the Plotly graph objects (`graph_objs`) are imported
to create a pie chart and the Plotly express (`px`) is imported to
create a scatter plot. Afther we have loaded the libraries and modules,
we load the dataset using `read_csv` method from Pandas, either from a
local file or from a remote URL, in this case I am exporting the data
from my Github repository.

The `app.layout` is where the components of the dashboard are defined
such as tables, dropdowns, graphs, and other HTML elements. Here, you
can be creative and write a layout that is both visually appealing and
functional. I am going for a simple design with a heather,
`html.H1('CPU Benchmark Data'),` and a slim line that works as separator
between the sections of the dashboard `html.Hr(),`. I start the
dashboard presenting a preview of the top-10 rows of the dataset using
the function `dash_table.DataTable()`. The function has several
arguments, but perhaps the most important one is the data source
`data=df.head(10).to_dict('records'),`which displays only the first 10
rows of the data.

After the data preview, I define another line `html.Br()`, to mark the
beginning of another section of the web application, followed by the
function, `html.H4('Histogram variable:')`, that displays a tittle of
the histogram. Next, I define a dropdown menu to select between each
column of the dataset:

`dcc.Dropdown(         id='variable-selector',         options=[{'label': i, 'value': i} for i in df.columns],         value='cpu_value(higher_is_better)'     )`

This is followed by two bottoms that are used to sort the table in an
ascending or descending manner according to the variable selected. This
snipped of code is the following one:

`dcc.RadioItems(         id='sort-order',         options=[{'label': i, 'value': i} for i in ['Ascending', 'Descending']],         value='Ascending',         labelStyle={'display': 'inline-block'}     )`

And finally, we display the histogram using the following function:

`dcc.Graph(         id='histogram',         figure={}     )`

The rest of the layout follows the same mechanics. I define a dropdown
menu, `dcc.Dropdown()`, to select a variable for the next plot then I
render the plot using the same `dcc.Graph()` function.

After defining the `app.layout`, we have to write the `app.callback`
decorator that is used to bind the input/output of the interactive
components (i.e., the dropdown menus) to the graph. Furthermore, the
`update_histogram_and_table`, `update_pie_chart`, and
`update_scatter_plot` functions that are the callback functions that
update the graph based on the user input.

``` python
import dash
from dash import dcc
from dash import html
from dash import dash_table
import pandas as pd
import plotly.graph_objs as go # for the pie chart
import plotly.express as px # for the scatter plot

external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

app = dash.Dash(__name__, external_stylesheets=external_stylesheets)

# Load the dataset
#df = pd.read_csv("test_cpus.csv")
df = pd.read_csv("https://raw.githubusercontent.com/Wario84/blog/main/assets/data/test_cpus.csv")

app.layout = html.Div([
    html.H1('CPU Benchmark Data'),
    html.Hr(),
    html.H3('Data Preview:'),
    dash_table.DataTable(
        id='table',
        columns=[{"name": i, "id": i} for i in df.columns],
        data=df.head(10).to_dict('records'),
        style_table={'overflowX': 'auto'},
        style_cell={'textAlign': 'left'},
        sort_action='native',
        page_action='none',
        style_data_conditional=[{
            'if': {'row_index': 'odd'},
            'backgroundColor': 'rgb(248, 248, 248)'
        }]
    ),
    html.Br(),
    html.H4('Histogram variable:'),
    dcc.Dropdown(
        id='variable-selector',
        options=[{'label': i, 'value': i} for i in df.columns],
        value='cpu_value(higher_is_better)'
    ),
    dcc.RadioItems(
        id='sort-order',
        options=[{'label': i, 'value': i} for i in ['Ascending', 'Descending']],
        value='Ascending',
        labelStyle={'display': 'inline-block'}
    ),
    dcc.Graph(
        id='histogram',
        figure={}
    ),
        html.Br(),
    html.H4('Pie-chart variable:'),
     dcc.Dropdown(
                id="variable-selector-2",
                options=[
                    {"label": "Ghz", "value": "ghz"},
                    {"label": "Cores", "value": "cores"},
                    {"label": "Threads", "value": "threads"},
                    {"label": "Year", "value": "year"},
                    #"ghz","cores","threads"

                ],
                #style={"width": "45%"}
                value="cores"
                
            ),
             dcc.Graph(id="pie-chart"),
             html.Br(),
    html.H4('Scatter-Plot variable:'),
    dcc.Dropdown(
        id='variable-selector-3',
        options=[{'label': i, 'value': i} for i in df.columns],
        value='cpu_name'
    ),
             
             dcc.Graph(id="scatter-plot"),
])

@app.callback(
    [dash.dependencies.Output('histogram', 'figure'),
     dash.dependencies.Output('table', 'data')],
    [dash.dependencies.Input('variable-selector', 'value'),
     dash.dependencies.Input('sort-order', 'value')]
)
def update_histogram_and_table(variable, sort_order):
    df_sorted = df.sort_values(by='cpu_value(higher_is_better)', ascending=False)
    if sort_order == 'Ascending':
        df_sorted = df_sorted.iloc[::-1]
    data_table = df_sorted.head(10).to_dict('records')

    fig = {
        'data': [{
            'x': df[variable],
            'type': 'histogram'
        }],
        'layout': {
            'title': 'Histogram of ' + variable,
            'xaxis': {'title': variable},
            'yaxis': {'title': 'Count'}
        }
    }

    return fig, data_table

@app.callback(
    dash.dependencies.Output("pie-chart", "figure"),
    [dash.dependencies.Input("variable-selector-2", "value")]
)

def update_pie_chart(selected_column):
    #filtered_df = df[df['year'] == selected_column]
    values = df[selected_column].value_counts().values
    labels = df[selected_column].value_counts().index
    fig = go.Figure(data=[go.Pie(labels=labels, values=values)])
    #fig.update_layout(title=f"{selected_column} distribution in {selected_column}")
    return fig

@app.callback(
    dash.dependencies.Output("scatter-plot", "figure"),
    [dash.dependencies.Input("variable-selector-3", "value")]
)
def update_scatter_plot(variable):
    return px.scatter(df, x="price_usd", y=variable).update_layout(
        xaxis={"title": "Price (USD)"},
        yaxis={"title": variable.capitalize()},
        margin={"l": 40, "b": 40, "t": 10, "r": 10},
        height=300,
    )

if __name__ == '__main__':
    app.run_server(debug=False)
```

## Deploying as a static website

To finally deploy the dashboard as web application, I am going to rely
on this video put forward by the people from Plotly:
<a href="https://www.youtube.com/watch?v=H16dZMYmvqo">Deploy your Python
Data App to the Web for Free - Dash</a>. The procedure is step by step,
and it very simple, first, we put the `.py` python script in a public
Github repository. Then we open an account on `render.com` and follow a
simple procedure.

## The final CPU Dashboard

Finally, I present you the CPU benchmark Dashboard. But for a better experience and visualization, I invite you to check out
the static website at <a href="https://cpu-benchmark-plotly-dash.onrender.com/">cpu-benchmark-plotly-dash.onrender.com</a>


<iframe src="https://cpu-benchmark-plotly-dash.onrender.com/" title="w" width="800px" height="600px" frameborder="50">
</iframe>


