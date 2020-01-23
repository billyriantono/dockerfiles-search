FROM ubuntu:18.10
RUN export DEBIAN_FRONTEND=noninteractive
ADD install.sh install.sh
RUN ./install.sh
RUN apt update && apt install -y g++
RUN mkdir /input /output
WORKDIR /output
ADD pdf.sh /pdf.sh
CMD /pdf.sh
