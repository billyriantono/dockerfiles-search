FROM jwilder/docker-gen:0.7.3
COPY templates  /etc/docker-gen/templates
# TODO: -notify-sighup isn't working. This means I have to restart nginx manually after an update. 
# I'm pretty sure this is because there isn't a container called technocore_nginx. 
CMD ["-notify-sighup", "technocore_nginx", "-watch", "-only-exposed", "/etc/docker-gen/templates/nginx.tmpl", "/etc/nginx/conf.d/default.conf"]
