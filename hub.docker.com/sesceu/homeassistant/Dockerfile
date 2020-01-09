FROM homeassistant/home-assistant:latest
MAINTAINER Sebastian Schneider <mail@sesc.eu>

# add non-free repos
RUN sed "s/\(deb .* main\)/\1 non-free/g" /etc/apt/sources.list

# install additional packages
RUN apt update && apt install -q -y \
    libttspico-utils \
    && rm -rf /var/lib/apt/lists/*
