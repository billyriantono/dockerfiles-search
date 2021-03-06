FROM ruby:2.6.5

LABEL author="Allan Batista <allan@allanbatista.com.br>"

# default sh as bash
SHELL ["/bin/bash", "-c"]

# no interaction
ENV DEBIAN_FRONTEND noninteractive
ENV TERM linux
ENV SLUGIFY_USES_TEXT_UNIDECODE=yes

# install dependencies
RUN apt-get update && \
    apt-get install locales apt-utils -y && \
    apt-get clean

# set default encode
RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "LANG=en_US.UTF-8" > /etc/locale.conf && \
    locale-gen en_US.UTF-8

# expose
EXPOSE 3000

# define default app location
ENV HOME_APP=/opt/app
RUN mkdir -p ${HOME_APP}
COPY . ${HOME_APP}
WORKDIR ${HOME_APP}

VOLUME ${HOME_APP}/storage

# install dependencies and build
RUN bundle install --without development test

# start up project
RUN chmod +x entrypoint.sh
ENTRYPOINT [ "/opt/app/entrypoint.sh" ]
CMD ["b2flow-api"]