FROM ubuntu:latest
RUN apt-get update && \ 
    apt-get install -y git
MAINTAINER Ninaj "ninja@ninja.com"
ENV APPDIR="/app/" \
    PATH="$PATH:$APPDIR" \
    STATE="Boo"
COPY ["book.sh", "book2.sh", "tst", "$APPDIR"]
ADD ["./junk.tar", "/"]
WORKDIR $APPDIR
LABEL team="t360" \
      engine="kubernetes" \ 
      cloud="aws" \
      env="dev"
ADD ["https://www.google.com","/boo"]
ENTRYPOINT ["/app/book.sh"]
