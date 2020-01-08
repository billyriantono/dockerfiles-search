FROM k8s.gcr.io/fluentd-elasticsearch:v2.2.0
RUN apt-get update && apt-get install -y iputils-ping
RUN apt-get install -y curl
RUN apt-get install -y vim
RUN gem install fluent-plugin-remote_syslog 
RUN gem install remote_syslog_sender
