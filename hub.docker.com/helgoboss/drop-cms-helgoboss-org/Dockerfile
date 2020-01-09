FROM helgoboss/drop-cms-fs-memcached

# Add fonts
ADD fonts /root/.fonts

# Update fonts cache
USER root
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y fontconfig

USER root
ENV HOME /root
RUN fc-cache -f -v