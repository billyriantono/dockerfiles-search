FROM rtfpessoa/ubuntu-jdk8
LABEL maintainer="Kyle Baldwin <kwb@mail.sfsu.edu>"

RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8
ENV DEBIAN_FRONTEND noninteractive

# Install java and curl and tar
RUN apt-get update && apt-get install -y curl tar

# Make app directories 
RUN mkdir -p /app/out /app/jdbc

# Download jasperstarter 
RUN curl -O -L -J https://sourceforge.net/projects/jasperstarter/files/JasperStarter-3.5/jasperstarter-3.5.0-bin.tar.bz2/download 
RUN tar xj -C /app -f jasperstarter-3.5.0-bin.tar.bz2

# Add jasperstarter to path 
ENV PATH="$PATH:/app/jasperstarter/bin"