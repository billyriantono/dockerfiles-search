FROM frekele/ant

MAINTAINER Instrumentisto Team <developer@instrumentisto.com>

ENV FLEXJS_HOME='/flexjs'
ARG FLEXJS_VERSION=0.8.0

# Install Flex SDK and its dependencies
RUN update-ca-certificates \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
            rsync \
            bzip2

RUN curl -fL -o /tmp/flexjs.tar.gz \
     http://www-eu.apache.org/dist/flex/flexjs/$FLEXJS_VERSION/binaries/apache-flex-flexjs-${FLEXJS_VERSION}-bin.tar.gz \
     && tar -xzf /tmp/flexjs.tar.gz -C /tmp \
     && mv /tmp/apache-flex-flexjs-* $FLEXJS_HOME \
     && mkdir /flexjs/in \
     && curl -fL -o /flexjs/in/apache-flex-falconjx-${FLEXJS_VERSION}-bin.zip \
http://www-eu.apache.org/dist/flex/falcon/$FLEXJS_VERSION/binaries/apache-flex-falconjx-${FLEXJS_VERSION}-bin.zip \
     && curl -fL -o /flexjs/in/AdobeAIRSDK.tbz2 \
     http://airdownload.adobe.com/air/mac/download/14.0/AdobeAIRSDK.tbz2

WORKDIR $FLEXJS_HOME

RUN ant -f installer.xml \
        -Dplatform="mac" \
        -Dinput.air.download=y \
        -Dinput.flash.download=y \
        -Dinput.flat.download=y

RUN chown -R root:root $FLEXJS_HOME \

 && apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
            bzip2 \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
           /tmp/*

ENV PATH="$FLEXJS_HOME/bin:$PATH"


# Install Flash Player and its dependencies
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
            libnss3 libgtk2.0-0 \
            xvfb xauth \

 && curl -fL -o /tmp/flash_player.tar.gz \
         https://fpdownload.macromedia.com/pub/flashplayer/updaters/27/flash_player_sa_linux_debug.x86_64.tar.gz \
 && tar -xzf /tmp/flash_player.tar.gz -C /tmp \
 && mv /tmp/flashplayerdebugger /usr/local/bin/ \
 && mkdir -p /usr/local/doc/flashplayerdebugger \
 && mv /tmp/LGPL/* /usr/local/doc/flashplayerdebugger/ \
 && chown -R root:root /usr/local/bin/flashplayerdebugger \
                       /usr/local/doc/flashplayerdebugger \

 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
           /tmp/*

# Create wrapper for xvfb-run command
RUN echo '#!/bin/sh'                                    >> /usr/local/bin/xvfb \
 && echo 'num=$(echo $DISPLAY | cut -d: -f2)'           >> /usr/local/bin/xvfb \
 && echo 'args="-screen 0 $RESOLUTION -ac +extension RANDR"' \
                                                        >> /usr/local/bin/xvfb \
 && echo 'xvfb-run -e /dev/stderr -n $num -s "$args" "$@"' \
                                                        >> /usr/local/bin/xvfb \
 && chmod +x /usr/local/bin/xvfb

ENV FLASH_PLAYER_EXE='/usr/local/bin/flashplayerdebugger' \
    DISPLAY=':99' \
    RESOLUTION='1024x768x24'


# Prepare application directory
RUN mkdir -p /app

WORKDIR /app

ENTRYPOINT []
CMD ["mxmlc","-version"]