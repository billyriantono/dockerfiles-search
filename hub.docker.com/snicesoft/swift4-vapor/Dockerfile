FROM swift:4.1

LABEL maintainer="snicesoft (zhuzheteng@gmail.com)"

RUN apt-get -qq update &&  \
    curl -sL apt.vapor.sh -o apt.vapor.sh && \
    bash ./apt.vapor.sh && \
    apt-get -y install vapor && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /vapor

VOLUME ["/vapor"]

EXPOSE 8080

# Launch the image with this command: 
# docker run -ti --rm --privileged=true --name vapor -p 127.0.0.1:8080:8080 -v $(pwd)/vapor/projects:/vapor vapor