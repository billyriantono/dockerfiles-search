FROM openshift/ruby-20-centos7

USER default
EXPOSE 8080

ENV RACK_ENV production
ENV RAILS_ENV production

ENV SOURCE_ROOT /opt/openshift/src
COPY . ${SOURCE_ROOT}/ruby-hello-world
WORKDIR ${SOURCE_ROOT}/ruby-hello-world

RUN scl enable ror40 "bundle install"
CMD ["scl", "enable", "ror40", "./run.sh"]
