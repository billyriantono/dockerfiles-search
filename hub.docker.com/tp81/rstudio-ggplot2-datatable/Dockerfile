## Start with the official rocker image providing 'rstudio'
FROM rocker/rstudio:latest

## This handle reaches the author
MAINTAINER "Thomas Pengo" thomas.pengo@gmail.com

# Add ggplot2
RUN echo "install.packages(\"ggplot2\")" | R --no-save

# Add data.table
RUN echo "install.packages(\"data.table\")" | R --no-save

EXPOSE 8787

## Expose a default volume for Kitematic 
VOLUME /home/rstudio

CMD ["/init"]
