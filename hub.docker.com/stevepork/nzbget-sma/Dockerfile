FROM linuxserver/nzbget
MAINTAINER Steven Chorkley

ENV GOROOT /usr/local/bin/golang
ENV GOPATH $HOME/go
ENV PATH $GOROOT/bin:$GOPATH/bin:$PATH
ENV RCLONE_VERSION=current

# get python3 and git, and install python libraries
RUN apk update && \
    apk add --no-cache \
      git \
      py-pip && \

# install pip, venv, and set up a virtual self contained python environment
    python -m pip install --user --upgrade pip && \
    python -m pip install --user virtualenv && \
    mkdir /usr/local/bin/sma && \
    python -m virtualenv /usr/local/bin/sma/env && \
    python /usr/local/bin/sma/env/bin/pip install requests \
      requests[security] \
      requests-cache \
      babelfish \
      'guessit<2' \
      'subliminal<2' \
      'stevedore==1.19.1' \
      python-dateutil \
      qtfaststart && \

# download repo
    git clone https://github.com/mdhiggins/sickbeard_mp4_automator.git /usr/local/bin/sma/sickbeard_mp4_automator && \

# create logging directory
    mkdir /var/log/sickbeard_mp4_automator && \
    touch /var/log/sickbeard_mp4_automator/index.log && \
    chgrp -R users /var/log/sickbeard_mp4_automator && \
    chmod -R g+w /var/log/sickbeard_mp4_automator && \
    
# copy NZBGetPostProcess to NZBGet scripts folder
    mkdir /app/nzbget/scripts && \
    cp /usr/local/bin/sma/sickbeard_mp4_automator/NZBGetPostProcess.py /app/nzbget/scripts/ && \

# ffmpeg
    wget https://johnvansickle.com/ffmpeg/builds/ffmpeg-git-amd64-static.tar.xz -O /tmp/ffmpeg.tar.xz && \
    mkdir /usr/local/bin/ffmpeg && \
    tar -xJf /tmp/ffmpeg.tar.xz -C /usr/local/bin/ffmpeg --strip-components 1 && \
    chgrp -R users /usr/local/bin/ffmpeg && \
    chmod g+x /usr/local/bin/ffmpeg/ffmpeg && \
    chmod g+x /usr/local/bin/ffmpeg/ffprobe && \

# cleanup
    rm -rf \
      /tmp/* \
      /var/lib/apt/lists/* \
      /var/tmp/*