FROM java:7
MAINTAINER Andres Pupiales <apupiales@gmail.com>

# Set customizable env vars defaults.
# Set Grails version (max version for this Docker image is: 2.5.6).
ENV GRAILS_VERSION 2.5.6

# Install Grails
WORKDIR /usr/lib/jvm
RUN wget https://github.com/grails/grails-core/releases/download/v$GRAILS_VERSION/grails-$GRAILS_VERSION.zip && \
    unzip grails-$GRAILS_VERSION.zip && \
    rm -rf grails-$GRAILS_VERSION.zip && \
    ln -s grails-$GRAILS_VERSION grails

# Setup Grails path.
ENV GRAILS_HOME /usr/lib/jvm/grails
ENV PATH $GRAILS_HOME/bin:$PATH

EXPOSE 8090

# Create App Directory
RUN mkdir /app

# Set Workdir
WORKDIR /app

RUN git clone https://github.com/ppazos/cabolabs-ehrserver.git . && \
    git checkout -b v1.1
