FROM dm3ll3n/shinystudio
#FROM ced9353b2b76

RUN apt-get update && apt-get install libcurl4-openssl-dev libv8-3.14-dev -y &&\
    apt-get install libgdal-dev -y &&\	
	apt-get install libudunits2-dev -y

RUN apt install libftgl2 libcgal-dev libglu1-mesa-dev libglu1-mesa-dev libx11-dev libfreetype6-dev -y
	
RUN R -e "install.packages('rgdal', repos = 'https://cloud.r-project.org')"
RUN R -e "install.packages('plotly', repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('ncdf4', repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('rgl', repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('units', repos = 'https://cloud.r-project.org')"
RUN R -e "install.packages('mapview', repos='http://cran.rstudio.com/', dependencies=T)"
RUN R -e "install.packages(c('sf', 'leafem'), repos='http://cran.rstudio.com/', dependencies = T)"
RUN R -e "install.packages(c('fasttime', 'shinyFiles'), repos = 'https://cloud.r-project.org')"
RUN R -e "install.packages(c('hydroGOF', 'hydroTSM'), repos = 'https://cloud.r-project.org', dependencies = T)"
