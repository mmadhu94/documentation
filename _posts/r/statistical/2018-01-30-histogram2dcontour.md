---
title: 2D Histogram Contour in R | Examples | Plotly
name: 2D Histogram Contour
permalink: r/2d-histogram-contour/
description: How to create 2D Histogram Contour plots in R with Plotly.
layout: base
thumbnail: thumbnail/hist2dcontour.png
language: r
has_thumbnail: true
display_as: statistical
order: 6
output:
  html_document:
    keep_md: true
---



### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.


```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.7.1.9000'
```

#### Basic 2D Histogram Contour


```r
library(plotly)

s <- matrix(c(1, -.75, -.75, 1), ncol = 2)
obs <- mvtnorm::rmvnorm(500, sigma = s)

p <- plot_ly(x = obs[,1], y = obs[,2]) %>% 
  add_trace(type='histogram2dcontour')

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link <- api_create(p, filename = "hist2dcontour-basic")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/5231.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

#### Styled 2D Histogram Contour


```r
library(plotly)

cnt <- with(diamonds, table(cut, clarity))

p <- plot_ly(diamonds, x = ~cut, y = ~clarity, z = ~cnt) %>%
  add_trace(
    type='histogram2dcontour',
    contours = list(
      showlabels = T,
      labelfont = list(
        family = 'Raleway',
        color = 'white'
      )
    ),
    hoverlabel = list(
      bgcolor = 'white',
      bordercolor = 'black',
      font = list(
        family = 'Raleway',
        color = 'black'
      )
    )
)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link <- api_create(p, filename = "hist2dcontour-styled")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/5237.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

#### 2D Histogram Contour Subplot


```r
library(plotly)

x <- rnorm(1000)
y <- rnorm(1000)
s <- subplot(
  plot_ly(x = x, color = I("black"), type = 'histogram'), 
  plotly_empty(), 
  plot_ly(x = x, y = y, type = 'histogram2dcontour', showscale = F), 
  plot_ly(y = y, color = I("black"), type = 'histogram'),
  nrows = 2, heights = c(0.2, 0.8), widths = c(0.8, 0.2), 
  shareX = TRUE, shareY = TRUE, titleX = FALSE, titleY = FALSE
)

p <- layout(s, showlegend = FALSE)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link <- api_create(p, filename = "hist2dcontour-subplot")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/5235.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

#### Reference

See [https://plot.ly/r/reference/#histogram2dcontour](https://plot.ly/r/reference/#histogram2dcontour) for more information and options!