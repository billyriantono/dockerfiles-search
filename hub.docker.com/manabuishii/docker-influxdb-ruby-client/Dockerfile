FROM ruby:2.3.1
RUN gem install influxdb -v=0.3.11
ADD influxdb_client.rb /
ENTRYPOINT ["ruby" , "/influxdb_client.rb"]
