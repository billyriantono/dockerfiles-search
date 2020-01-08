FROM mohamnag/gradle-psql
MAINTAINER Mohammad Naghavi <mohamnag@gmail.com>

RUN apt-get update && \
    apt-get install -y maven

# clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*    
