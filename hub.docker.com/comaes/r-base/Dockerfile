FROM rocker/shiny

# RUN rm -rf /var/lib/apt/lists/*
RUN apt-get update
RUN  apt-get install -y libssl-dev
#install R dependencies
RUN  R -e "install.packages('devtools', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('httr', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('rjson', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('reshape', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('reshape2', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('xts', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('shiny', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('shinydashboard', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('plyr', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('dplyr', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('RCurl', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('doMC', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('foreach', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('ggplot2', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('dygraphs', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('lubridate', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('scales', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('uuid', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('DT', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('stringr', repos='http://cran.rstudio.com/')"
RUN  R -e "install.packages('tidyr', repos='http://cran.rstudio.com/')"


#run server
CMD ["/usr/bin/shiny-server.sh"]
