FROM debian

ENV \
     GALAXY_USER=galaxy \
     GALAXY_USER_UID=999 \
     GALAXY_USER_GID=666 \
     GALAXY_HOME=/home/galaxy

# Install Galaxy environment
RUN apt-get update \
 && apt-get install -y python3-minimal python3-urllib3 python3-pip \
                       git curl postgresql-client libgcc-8-dev \
                       watchdog \
 && ln -sf /usr/bin/python3 /usr/bin/python \
 && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN apt-get update && apt-get install -y libpq-dev

RUN python3 -m pip install pyyaml

# Production Environment for Galaxy
RUN groupadd -g $GALAXY_USER_GID -r $GALAXY_USER &&\
    useradd -r -g $GALAXY_USER --uid $GALAXY_USER_UID -m -d $GALAXY_HOME -c "Galaxy user" $GALAXY_USER

WORKDIR /galaxy
ENTRYPOINT ["sh", "run.sh"]
