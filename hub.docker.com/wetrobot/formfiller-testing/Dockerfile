

from rocker/tidyverse


maintainer "Currently Joonas Miettinen" app@cancer.fi


run apt-get update && apt-get install -y \
    r-cran-rjava \
    default-jdk \
    libcurl4-openssl-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    libgeos-dev


run R CMD javareconf


## from fcrbase:master@cb904620e69ebdbad31e9145843c2980ed073ddb
run R -e 'options(warn = 2); install.packages(c("shiny", "data.table", "rJava", "xlsx", "DT", "ggplot2", "assertthat",  "shinyjs", "shinyBS", "markdown", "testthat", "git2r", "rmarkdown",  "devtools", "raster", "maptools", "rgeos", "htmltools", "gridExtra",  "png"))'


run R -e 'options(warn = 2); devtools::install_github("rstudio/shinytest")'
run R -e 'options(warn = 2); webdriver::install_phantomjs()'


