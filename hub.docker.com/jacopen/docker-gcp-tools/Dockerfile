FROM google/cloud-sdk:latest

RUN apt install -y jq
### knctl ####
RUN curl -vL https://github.com/cppforlife/knctl/releases/download/`curl -s https://api.github.com/repos/cppforlife/knctl/releases/latest | jq -r .tag_name`/knctl-linux-amd64 -o /usr/local/bin/knctl &&\
    chmod +x /usr/local/bin/knctl
    
### riff CLI ####
RUN curl -vL https://github.com/projectriff/riff/releases/download/v0.1.3/riff-linux-amd64.tgz | tar zxvf - &&\
    cp ./riff /usr/local/bin/ &&\
    rm ./riff

