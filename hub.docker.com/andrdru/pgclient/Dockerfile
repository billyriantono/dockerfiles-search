FROM debian:jessie

RUN apt-get update

# Install Git
RUN apt-get install -y postgresql-client

#Install curl
RUN apt-get install -y curl libcurl3 libcurl3-dev

#Install International Components for Unicode
RUN apt-get install -y libicu-dev

#ssl libs
RUN apt-get install -y libc-client-dev libkrb5-dev

#cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#new entrypoint
COPY entrypoint.sh /usr/local/bin/

RUN chmod 777 /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]