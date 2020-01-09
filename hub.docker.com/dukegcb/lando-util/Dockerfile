FROM python:3.6
LABEL maintainer="dan.leehr@duke.edu"

RUN mkdir -p /app
COPY . /app
RUN pip install /app
WORKDIR /app

# Create a default user and home directory
ENV HOME=/home/lando-util
# home dir is created by useradd with group (g=0) to comply with
# https://docs.openshift.com/container-platform/3.11/creating_images/guidelines.html#openshift-specific-guidelines
RUN useradd -u 1001 -r -g 0 -m -d ${HOME} -s /sbin/nologin \
      -c "Default Lando Util User" lando_util && \
  chown -R 1001:0 /app && \
  chmod g+rwx ${HOME}

USER lando_util
