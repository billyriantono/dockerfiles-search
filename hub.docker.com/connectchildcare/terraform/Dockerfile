FROM hashicorp/terraform as terraform

FROM node:12

RUN apt-get update && \
    apt-get install -y postgresql-client python3-pip && \
    pip3 install awscli && \
    npm install -g serverless && \
    apt-get remove -y python3-pip && \
    apt-get clean

COPY --from=terraform /bin/terraform /bin/terraform

RUN mkdir /app
WORKDIR /app

ENTRYPOINT ["/bin/bash"]

