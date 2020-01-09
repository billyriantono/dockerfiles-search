FROM debian:stretch

RUN apt-get update && apt-get install \
	fabric -y

ADD fabfile.py /bin/

ADD main.sh /bin/
RUN chmod +x /bin/main.sh

# Set default env vars
ENV PLUGIN_SOURCE . 
ENV PLUGIN_STRATEGY one_at_a_time
ENV PLUGIN_POOL_SIZE 3

ENTRYPOINT /bin/main.sh