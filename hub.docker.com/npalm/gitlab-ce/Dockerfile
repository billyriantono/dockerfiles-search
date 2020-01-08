FROM gitlab/gitlab-ce:8.5.1-ce.0
MAINTAINER Niek Palm <dev.npalm@gmail.com>

COPY assets/wrapper /usr/local/bin/

# Copy assets
COPY assets/wrapper /usr/local/bin/

# Wrapper to handle signal, trigger runit and reconfigure GitLab
CMD ["/usr/local/bin/wrapper"]
