FROM rocker/shiny:latest

# Install Python
RUN \
  apt-get update && \
  apt-get install -y python3 python3-pip

RUN pip3 install --upgrade pip
RUN pip3 install gensim textblob

# Install additional R
RUN apt-get install -y libssl-dev libxml2-dev libgsl0-dev
RUN R -e "install.packages(c('Rccp', 'RcppEigen', 'Matrix'))"
RUN R -e "install.packages(c('RSpectra', 'reticulate'))"

RUN R -e "install.packages(c( \
  'devtools', 'shinydashboard', 'wordcloud2', 'LDAvis', \
  'dplyr', 'tidytext', 'topicmodels', 'plotly', \
  'stringr', 'quanteda', 'DT' \
  ), repos='https://cran.rstudio.com/')"

RUN R -e 'install.packages(c("lexicon"))'
RUN R -e 'devtools::install_github("AnalytixWare/ShinySky", )'
RUN R -e 'devtools::install_github("hadley/ggplot2")'
