FROM alpine:3.7

RUN apk add --update --no-cache python py-pip 
RUN pip install --upgrade awscli
RUN pip install cfn-lint --upgrade

CMD ["/bin/bash"]
