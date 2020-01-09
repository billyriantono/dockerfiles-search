FROM ubuntu:trusty
RUN apt-get update -y && apt-get install -y postgresql postgresql-contrib python-psycopg2 curl git
RUN (addgroup --system --gid 498 jenkins)
RUN (adduser --system --uid=498 --gid=498 --shell /bin/bash jenkins)
VOLUME /gopath/src/sevelin-locker-server-go
RUN \
  mkdir -p /goroot && \
  curl https://storage.googleapis.com/golang/go1.5.1.linux-amd64.tar.gz | tar xvzf - -C /goroot --strip-components=1
# Set environment variables.
ENV GOROOT /goroot
ENV GOPATH /gopath
ENV PATH $GOROOT/bin:$GOPATH/bin:$PATH
# Define working directory.
WORKDIR /gopath
RUN chown -R jenkins:jenkins /goroot/
RUN chown -R jenkins:jenkins /gopath/
RUN echo "nameserver 8.8.8.8" > /etc/resolv.conf

# Define default command.
CMD ["bash"]
