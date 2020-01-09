FROM openanalytics/r-base

# system libraries of general use
RUN apt-get update && apt-get install -y \
  sudo \
  pandoc \
  pandoc-citeproc \
  libcurl4-gnutls-dev \
  libcairo2-dev \
  libssl-dev \
  libssh2-1-dev \
  libssl1.0.0 \
  libxml2-dev \
  libmysqlclient20 \
  libmariadb-dev

# Install packages
RUN R -e 'install.packages("remotes")'
RUN R -e 'remotes::install_cran("shiny")'
RUN R -e 'remotes::install_cran("shinydashboard")'
RUN R -e 'remotes::install_cran("shinydashboardPlus")'
RUN R -e 'remotes::install_cran("rmarkdown")'
RUN R -e 'remotes::install_cran("markdown")'
RUN R -e 'remotes::install_cran("golem")'
RUN R -e 'remotes::install_cran("shinyWidgets")'
RUN R -e 'remotes::install_cran("bsplus")'
RUN R -e 'remotes::install_cran("DT")'
RUN R -e 'remotes::install_cran("dplyr")'
RUN R -e 'remotes::install_cran("rlang")'
RUN R -e 'remotes::install_cran("stringr")'
RUN R -e 'remotes::install_cran("tidyr")'
RUN R -e 'remotes::install_cran("lubridate")'
RUN R -e 'remotes::install_cran("pool")'
RUN R -e 'remotes::install_cran("RMariaDB")'
