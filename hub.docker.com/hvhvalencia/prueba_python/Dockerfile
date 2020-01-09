FROM ubuntu
RUN apt update
RUN apt install -y nano
RUN apt install -y firefox
RUN apt install -y python && apt install -y git
RUN mkdir /datos

WORKDIR /datos
RUN touch f1.txt

ENTRYPOINT ["/bin/bash"]
