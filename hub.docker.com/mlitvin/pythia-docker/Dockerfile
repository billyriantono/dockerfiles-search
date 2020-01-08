FROM golang

RUN mkdir /pythia && \
    cd /pythia && \
    GOPATH=/pythia go get github.com/fzipp/pythia && \
    ln -s /pythia/bin/pythia /usr/local/bin

EXPOSE 8080

ADD pythia_wrapper /usr/bin/
ADD run_pythia /root/

ENTRYPOINT [ "/usr/bin/pythia_wrapper" ]

CMD [ "-h" ] 

