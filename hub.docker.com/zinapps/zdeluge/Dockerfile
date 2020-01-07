FROM ubuntu
LABEL maintainer="Sarfaraz Ali Khan mrkhan1417@gmail.com"

RUN apt update && apt upgrade -y && \
    apt install software-properties-common -y && \
    add-apt-repository ppa:deluge-team/stable -y && \
    apt update && \
    apt install deluged deluge-webui -y
	
EXPOSE 8112
CMD ["deluge-web", "-d"]
