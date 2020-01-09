FROM logstash:1.5.6
# Composed through combination of http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Tools.DynamoDBLogstash.html and https://hub.docker.com/r/mantika/logstash-dynamodb-streams/~/dockerfile/

# Make .m2 accessible to logstash user, otherwise logstash won't start
RUN mkdir -p /var/lib/logstash/.m2
RUN ln -s /var/lib/logstash/.m2 /root/.m2

ENV PATH /opt/logstash/vendor/jruby/bin/:$PATH

RUN curl --create-dirs -sS -o /opt/logstash/vendor/jruby/lib/ruby/.mvn/extensions.xml https://raw.githubusercontent.com/takari/ruby-maven/master/.mvn/extensions.xml

RUN gem install logstash-input-dynamodb logstash-output-elasticsearch logstash-output-stdout

RUN plugin install logstash-input-dynamodb logstash-output-elasticsearch logstash-output-stdout
