FROM ubuntu:16.04

RUN apt-get update && apt-get upgrade && \
    apt-get install -y sudo && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install vim wget gcc build-essential \
    python3 tmux -y

# MP2
RUN apt-get install iptables net-tools -y
