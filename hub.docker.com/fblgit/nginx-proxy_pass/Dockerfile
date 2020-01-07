FROM ubuntu:16.04
RUN apt-get update && apt-get install nginx-full puppet bwm-ng wget curl dstat vim puppet-module-puppetlabs-apt -qy
RUN puppet module install jfryman-nginx
COPY start.sh /start.sh
COPY provision.pp /provision.pp
CMD ["/start.sh"]
