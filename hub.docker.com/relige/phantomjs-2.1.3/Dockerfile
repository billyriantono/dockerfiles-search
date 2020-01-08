FROM debian:jessie

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

# Set timezone
RUN echo "Europe/Moscow" > /etc/timezone && \
    dpkg-reconfigure --frontend noninteractive tzdata

# Create a default user
RUN useradd automation --shell /bin/bash --create-home

# Update the repositories
# Install utilities
# Install XVFB and TinyWM
# Install fonts
# Install git
# Install python-setuptools
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        wget \
        xvfb tinywm \
        build-essential chrpath libssl-dev libxft-dev \
        libfreetype6 libfreetype6-dev \
        libfontconfig1 libfontconfig1-dev \
        fonts-ipafont-gothic xfonts-100dpi xfonts-75dpi xfonts-scalable xfonts-cyrillic \
        python-pip \
    && rm -rf /var/lib/apt/lists/*

# Install Supervisor
RUN pip install supervisor

# Install PhantomJs
RUN wget https://github.com/ariya/phantomjs/releases/download/2.1.3/phantomjs \
    && mv phantomjs /usr/local/bin

# Configure Supervisor
ADD ./etc/supervisord.conf /etc/
ADD ./etc/supervisor /etc/supervisor

ENV DISPLAY :20.0
ENV SCREEN_GEOMETRY "1440x900x24"

EXPOSE 8910

VOLUME [ "/var/log/supervisor" ]

CMD ["/usr/local/bin/supervisord", "-c", "/etc/supervisord.conf"]