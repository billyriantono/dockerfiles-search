FROM debian

RUN apt-get update && apt-get install -y tidy
COPY tidy.conf /etc/tidy.conf
CMD [ "/bin/sh" ]
