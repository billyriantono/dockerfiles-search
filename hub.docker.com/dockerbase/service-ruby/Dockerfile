# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Service-ruby Image Container

FROM dockerbase/service

# Run dockerbase script
ADD     devbase-rvm.sh /dockerbase/
RUN     /dockerbase/devbase-rvm.sh

ENV     RVM_DIR /usr/local/rvm/
ENV     PATH $PATH:$RVM_DIR/bin

# Run dockerbase script
ADD     rvm.sh /dockerbase/
RUN     /dockerbase/rvm.sh

# Run dockerbase script
ADD     ruby.sh /dockerbase/
RUN     /dockerbase/ruby.sh
