ARG RUBY_VERSION=2.5.0
FROM centos:7
ARG RUBY_VERSION

# Configure the main working directory.
# This is the base directory used in any further RUN, COPY, and ENTRYPOINT commands.
ENV APP_HOME /var/centos7_ruby
RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME

# Copy the main application.
COPY . .

# Timezone
RUN rm /etc/localtime && ln -s /usr/share/zoneinfo/America/Los_Angeles /etc/localtime

# Centos dependencies
RUN bash -l docker/yum-install.sh

RUN adduser -ms /bin/bash evt; \
  chown -R evt: .

USER evt

# Install RVM
RUN bash -l -c "docker/install-rvm.sh 'stable'"
# RUN bash -l -c "rvm requirements 2.4.2"

# Install Ruby
# CMD bash -l su - evt
RUN bash -l -c "docker/install-ruby.sh 2.4.2"
RUN bash -l -c "docker/install-ruby.sh $RUBY_VERSION"
RUN bash -l -c "docker/set-path.sh $RUBY_VERSION"

# Node, bundler, gems
# RUN bash -l docker/install-app.sh

# Expose port 3000 and 8888 to the Docker host, so we can access it from the outside.
#EXPOSE 3000 8086
# EXPOSE 22 2226
