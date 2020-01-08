FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y ruby
COPY . /src/sh
RUN cd /src/sh && ./setup.sh
CMD ["/bin/bash"]
