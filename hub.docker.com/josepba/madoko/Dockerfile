FROM raabf/latex-versions:texlive2018

RUN apt update -y && \
    apt install -y curl inotify-tools xzdec && \
    curl -L https://git.io/n-install | bash -s -- -y

COPY instaler.sh /tmp
RUN chmod a+x /tmp/instaler.sh && /tmp/instaler.sh 

