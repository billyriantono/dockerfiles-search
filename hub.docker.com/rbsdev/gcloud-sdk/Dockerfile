FROM google/cloud-sdk:258.0.0

# Use ${DOLLAR} to scape environment variables: https://stackoverflow.com/a/24964089/2740179
ENV DOLLAR='$'

RUN apt-get -y install gettext-base \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
