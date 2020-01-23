FROM 4armed/ruby:2.3.4
MAINTAINER Marc Wickenden <marc@4armed.com>

RUN git clone https://github.com/iagox86/dnscat2.git /app

EXPOSE 53/udp

WORKDIR /app/server
RUN bundle install
CMD ruby ./dnscat2.rb $DOMAIN

# docker run -p 53:53/udp -ti --rm -e DOMAIN=yourdomain.com 4armed/dnscat2
