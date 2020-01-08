FROM weinstein/webserver:latest
USER root
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget
COPY install.sh .
RUN ./install.sh
