FROM ruby
LABEL Author="Lance Haig"

RUN gem install cassandra-web
COPY run.sh /
RUN chmod +x /run.sh

CMD ["/run.sh"]