FROM tony19/ruby
MAINTAINER Tony Trinh <tony19@gmail.com>

ARG USERNAME=app
ARG GEMSET=mygems

# tony19/ruby defaults to non-root
USER root

# TODO: Move Postgres and Redis servers to own containers
RUN apt-get update
RUN apt-get install -y \
    git           \
    libpq-dev     \
    nodejs        \
    postgresql    \
    redis-server  \
    vim

USER ${USERNAME}

# XXX: This command needs the Postgres server to be available...
# RUN sudo -u postgres psql -c "CREATE USER ${USERNAME} WITH SUPERUSER LOGIN;"

RUN /bin/bash -l -c "rvm gemset create ${GEMSET}"
RUN /bin/bash -l -c "gem install bundler foreman --no-ri --no-rdoc"

# Upgrade rubygems to fix foreman error: "`method_missing': undefined method `this'"
# http://stackoverflow.com/a/39475786/6277151
RUN /bin/bash -l -c "rvm rubygems 2.6.3"

EXPOSE 3000
ADD scripts /scripts
