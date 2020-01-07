# https://github.com/elastic/elasticsearch-docker
FROM docker.elastic.co/elasticsearch/elasticsearch:7.4.2

COPY ./config    /usr/share/elasticsearch/config/

# Add your elasticsearch plugins setup here
# Example: RUN elasticsearch-plugin install analysis-icu

ARG AWS_ACCESS_KEY_ID=Q8QXHKS2RHDPITWQUJUI
ARG AWS_SECRET_ACCESS_KEY=Neky32BEedyXrSewG6kTdAgssBlgt1cx9hEzUuT0


RUN elasticsearch-plugin install --batch repository-s3
RUN bin/elasticsearch-keystore create
RUN echo "$AWS_ACCESS_KEY_ID"| bin/elasticsearch-keystore add --stdin s3.client.default.access_key
RUN echo "$AWS_SECRET_ACCESS_KEY"| bin/elasticsearch-keystore add --stdin s3.client.default.secret_key