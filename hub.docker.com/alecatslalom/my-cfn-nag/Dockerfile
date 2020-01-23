FROM jenkinsci/jnlp-slave:alpine

USER root

ENV PATH="/app:${PATH}"
ENV OUTPUT_DIR="."

RUN apk add ruby ruby-rdoc
RUN gem install cfn-nag
ADD my-cfn-nag /app/
RUN chmod +x /app/my-cfn-nag

USER ${user}
RUN mkdir /workspace
WORKDIR /workspace

ENTRYPOINT ["/bin/bash", "/app/my-cfn-nag"]
