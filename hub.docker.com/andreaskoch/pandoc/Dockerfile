FROM phusion/baseimage:latest

MAINTAINER Andreas Koch <andy@ak7.io>

# Set correct environment
ENV HOME /root

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
RUN /usr/sbin/enable_insecure_key

# Install pandoc
ENV PANDOCVERSION 1.13.1
RUN apt-get -qy update && apt-get install -qy haskell-platform
RUN cabal update
RUN cabal install pandoc
RUN ln -s /root/.cabal/bin/pandoc /bin/pandoc

RUN mkdir -p /source
WORKDIR /source

ENTRYPOINT ["/bin/pandoc"]
CMD ["--help"]
