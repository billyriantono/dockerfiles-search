from rocker/rstudio

RUN apt-get update \
  && apt-get install -y --no-install-recommends libxml2-dev zlib1g-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/

RUN R -e "install.packages('tidyverse')"
