FROM java:6
MAINTAINER CROWDCODE <develop@crowdcode.io>

# Derived from mozart/grails by Manuel Ortiz Bey
# Set customizable env vars defaults.
# Set Grails version (max version for this Docker image is: 2.5.3).
ARG GRAILS_VERSION=2.2.1
ARG USER_ID=1000
ARG WORKSPACE_DIR="/workspace"

ENV GRAILS_VERSION ${GRAILS_VERSION}

# Install Grails
WORKDIR /usr/lib/jvm
RUN wget https://github.com/grails/grails-core/releases/download/v$GRAILS_VERSION/grails-$GRAILS_VERSION.zip && \
    unzip grails-$GRAILS_VERSION.zip && \
    rm -rf grails-$GRAILS_VERSION.zip && \
    ln -s grails-$GRAILS_VERSION grails

# Setup Grails path.
ENV GRAILS_HOME /usr/lib/jvm/grails
ENV PATH $GRAILS_HOME/bin:$PATH

# Create Workspace Directory
RUN mkdir $WORKSPACE_DIR

RUN useradd -ms /bin/bash  grailshome

# Set Workdir
WORKDIR $WORKSPACE_DIR

USER ${USER_ID}

RUN echo n | grails

# Copy entrypoint script
COPY src/entrypoint.sh /usr/local/bin/entrypoint.sh

# Set Default Behavior
ENTRYPOINT ["entrypoint.sh"]

CMD ["bash"]
