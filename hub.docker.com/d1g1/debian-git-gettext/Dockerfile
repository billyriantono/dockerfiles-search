FROM debian:stable-slim

ENV DEBIAN_FRONTEND noninteractive

RUN mkdir -p /root/work
WORKDIR /root/work/

RUN apt-get update && apt-get install --yes git gettext
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /usr/share/man/?? /usr/share/man/??_*

CMD ["bash"]
