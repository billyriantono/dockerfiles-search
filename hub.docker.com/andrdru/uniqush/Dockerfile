FROM debian:jessie

RUN apt-get update

#Install curl
#RUN apt-get install -y curl libcurl3 libcurl3-dev
RUN apt-get install wget -y

#RUN apt-get upgrade -y

RUN wget https://github.com/uniqush/uniqush-push/releases/download/2.3.0/uniqush-push_2.3.0_amd64.deb
RUN dpkg -i uniqush-push_2.3.0_amd64.deb

#cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


ENTRYPOINT /usr/bin/uniqush-push;