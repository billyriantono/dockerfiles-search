FROM ruby:latest

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y locales

RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8 

ENV LC_ALL="en_US.UTF-8"

RUN localedef -i en_US -f UTF-8 en_US.UTF-8 && \
    mkdir -p  "/to-compile" && \
    gem update --system && \
    gem install compass

VOLUME [ "/to-compile" ]

WORKDIR "/to-compile"

ENTRYPOINT [ "/usr/local/bundle/bin/compass" ]

CMD [ "version" ]
