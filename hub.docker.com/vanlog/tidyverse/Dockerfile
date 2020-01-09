FROM vanlog/r-base:R-3.4.4

MAINTAINER Andrea Melloncelli "andrea.melloncelli@vanlog.it"

# system library dependency for the tidyverse
RUN apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev 

# tidyverse
RUN R -e "install.packages('devtools', repos='https://cloud.r-project.org/')"
RUN R -e "install.packages('tidyverse', repo='http://cran.rstudio.com')"
RUN R -e "install.packages('future', repos='https://cloud.r-project.org/')"

CMD ["R"]
