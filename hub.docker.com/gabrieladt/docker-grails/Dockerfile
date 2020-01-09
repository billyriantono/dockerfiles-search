from gabrieladt/oracle-jre7

# Set customizable env vars defaults.
# Set Grails version (max version for this Docker image is: 2.5.0).
ENV GRAILS_VERSION 2.2.2

# Install Grails
WORKDIR /usr/lib/jvm
RUN wget --waitretry=1 --read-timeout=10 --timeout=5 -t 5 https://s3.amazonaws.com/gb-grails/grails-${GRAILS_VERSION}.zip

RUN unzip grails-$GRAILS_VERSION.zip
RUN rm -rf grails-$GRAILS_VERSION.zip
RUN ln -s grails-$GRAILS_VERSION grails

# Setup Grails path.
ENV GRAILS_HOME /usr/lib/jvm/grails
ENV PATH $GRAILS_HOME/bin:$PATH

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

