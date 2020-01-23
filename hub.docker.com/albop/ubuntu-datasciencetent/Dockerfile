FROM ubuntu:16.04
RUN apt-get update && apt-get upgrade -y
RUN apt-get install software-properties-common -y
RUN apt-add-repository ppa:kdenlive/kdenlive-stable -y
RUN apt-get update && apt-get upgrade -y
ENTRYPOINT ["kdenlive"]
