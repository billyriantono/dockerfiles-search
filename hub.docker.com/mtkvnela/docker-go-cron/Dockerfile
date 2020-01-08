FROM alpine:latest
LABEL maintainer="Johannes Schickling <schickling.j@gmail.com>"

ADD install.sh install.sh
RUN sh install.sh && rm install.sh


ENV SCHEDULE '*/30 * * * * *'
ENV PORT 8080
ENV COMMAND 'echo hii'

ADD run.sh run.sh

CMD ["bash", "run.sh"]
