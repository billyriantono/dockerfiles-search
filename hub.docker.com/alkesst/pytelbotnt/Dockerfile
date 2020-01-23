FROM maven:3.3.9

ENV aws_cli=1.11.136

RUN apt-get update && apt-get install -y jq python-pip python-dev

# Install AWS-CLI
RUN pip install awscli==${aws_cli}
