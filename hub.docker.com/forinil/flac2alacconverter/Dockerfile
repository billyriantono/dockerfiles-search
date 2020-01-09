FROM ubuntu:latest

VOLUME /alac
VOLUME /flac
WORKDIR /flac

ADD convert.sh /bin/convert.sh
RUN chmod +x /bin/convert.sh

RUN apt-get update
RUN apt-get install -y ffmpeg
RUN apt-get clean
RUN apt-get autoremove -y

ENTRYPOINT ["/bin/convert.sh"]
