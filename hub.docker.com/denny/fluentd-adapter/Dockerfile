# https://hub.docker.com/r/fluent/fluentd/~/dockerfile/
##  Build docker image: docker build --no-cache -t denny/fluentd-adapter:latest --rm=true .

FROM fluent/fluentd:v1.2

# Install out-http-ext fluentd output plugin, which is missing by default
RUN fluent-gem install fluent-plugin-out-http-ext

# Patch fluent source code for rfc5424 parsing issue.
# TODO: send out a PR to fluent github repo, and remove this workaround
ADD in_syslog.rb /usr/lib/ruby/gems/2.4.0/gems/fluentd-1.2.3/lib/fluent/plugin/in_syslog.rb
