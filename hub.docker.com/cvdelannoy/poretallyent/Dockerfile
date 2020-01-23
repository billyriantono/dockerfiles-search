FROM ubuntu:latest

RUN apt-get update && apt-get install -y curl
RUN curl -o /tmp/schema.tar.gz -L https://github.com/citation-style-language/schema/archive/v1.0.1.tar.gz
RUN cd /tmp && tar zxvf /tmp/schema.tar.gz

FROM ubuntu:latest

COPY --from=0 /tmp/schema-1.0.1 /var/csl/schema

RUN apt-get update && apt-get install -y jing

CMD ["bash"]
