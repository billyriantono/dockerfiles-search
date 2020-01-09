FROM ubuntu
MAINTAINER Damian Szymczuk (dszymczuk)
RUN apt-get update && apt-get install -y stress
ENTRYPOINT ["/usr/bin/stress"]
CMD ["-c", "2", "-t", "60"]
