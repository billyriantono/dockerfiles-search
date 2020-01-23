FROM circleci/elixir:1.9-node

RUN sudo apt-get update && \
    sudo apt-get upgrade -y

# Install the dependencies
RUN sudo apt-get install -y python-dev python-pip

# Install the latest awscli
RUN pip install awscli awsebcli --upgrade --user

# Install hex and rebar
RUN mix local.hex --force && \
    mix local.rebar --force
