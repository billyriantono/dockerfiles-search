FROM r-base:3.5.3

# libs are needed by devtools and stringr
RUN apt-get update && apt-get install -y build-essential libcurl4-gnutls-dev libxml2-dev libssl-dev libv8-dev

# install our dependencies.
COPY install /install
RUN Rscript /install/devtools.R
RUN Rscript /install/fg.R

# copy our app
COPY /app /app
COPY /LICENSE /app/
COPY /LICENSE-THIRD-PARTY /app/

WORKDIR /app
ENTRYPOINT Rscript main.R
