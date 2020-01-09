FROM r-base:3.5.1

COPY textanalyticshelpers /textanalyticshelpers

RUN \
    apt-get update \
    # spacy
    && apt-get install -y python-pip \
    && pip install -U spacy \
    && python -m spacy download en \
    # install dependencies for R packages
    && apt-get install -y \
        libxml2-dev \
        gfortran \
        libpng-dev\
        libglu1-mesa-dev \
        freeglut3-dev \
        mesa-common-dev \
        bwidget \
        libcurl4-openssl-dev \
        libssl-dev \
        libgsl-dev \
        default-jdk \
        liblzma-dev \
        libbz2-dev \
        libgdal-dev \
        libproj-dev \
        libcairo2-dev libxt-dev \
        libgmp-dev \
        libudunits2-dev \
    # install R packages required
    && R CMD javareconf \
    && install2.r --error \ 
        shiny shinyBS shinythemes \
        devtools \
        glue \
        tidyverse \
        slam \
        topicmodels LDAvis \
        wordcloud2 \
        DT \
        textstem cleanNLP \
        reticulate \
        widyr \
        broom \
    && R CMD build /textanalyticshelpers \
    && R CMD INSTALL textanalyticshelpers \
    && rm $(ls textanalyticshelpers_*.tar.gz) \
    && rm -rf /textanalyticshelpers \
    # directory to store the shiny app
    && mkdir -p /app/textanalytics \
    # make shiny run on port 3838
    && echo "local({options(shiny.port = 3838, shiny.host = '0.0.0.0')})" >> /usr/lib/R/etc/Rprofile.site \
    && apt-get update \
    # make image smaller
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

COPY ui.R /app/textanalytics
COPY server.R /app/textanalytics

EXPOSE 3838

CMD ["R", "-e", "shiny::runApp('/app/textanalytics')"]