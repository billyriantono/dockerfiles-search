FROM ubuntu:14.04

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:learningequality/kolibri && \
    apt-get update
RUN apt-get install -y kolibri

# RUN groupadd --gid 1000 app \
#   && useradd --uid 1000 --gid app --shell /bin/bash --create-home app

ENV USER=kolibri
USER kolibri

CMD ["kolibri", "start", "--foreground"]
