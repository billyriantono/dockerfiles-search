# https://github.com/lambci/docker-lambda#documentation
FROM lambci/lambda:build-provided
RUN yum install -y jq
RUN yum install -y postgresql-devel
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs \
 | sh -s -- -y --profile minimal --default-toolchain nightly
ADD build.sh /usr/local/bin/
VOLUME ["/code"]
WORKDIR /code
ENTRYPOINT ["/usr/local/bin/build.sh"]
