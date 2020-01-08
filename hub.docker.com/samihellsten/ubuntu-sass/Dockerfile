FROM ubuntu
LABEL maintainer="dropa@dropa.net"

# Install sass for compiling and git for automated pipelines
# to push compiled version in to the repository.
# locales is required for setting UTF-8.
RUN apt update && apt install -y git sass locales

# Set the locale.
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

# Default working directory.
WORKDIR /app

CMD ["scss"]
