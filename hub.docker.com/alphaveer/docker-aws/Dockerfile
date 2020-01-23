FROM docker:latest
RUN apk add openssh git jq py-pip ca-certificates iptables bash
RUN pip install -U pip awscli ecs-deploy aws-shell
CMD ["aws-shell"]
