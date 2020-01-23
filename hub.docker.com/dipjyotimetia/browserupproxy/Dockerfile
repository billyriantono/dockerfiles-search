FROM openjdk:8

ENV version=2.0.1

RUN wget https://github.com/browserup/browserup-proxy/releases/download/v${version}/browserup-proxy-${version}.tar
RUN tar xvf browserup-proxy-${version}.tar
RUN ln -s browserup-proxy-${version} browserup-proxy

CMD ["browserup-proxy/bin/browserup-proxy"]
