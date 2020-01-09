FROM alpine

COPY sample.txt /sample.txt

RUN apk add --no-cache git build-base && \
    git clone https://github.com/philips/text2pdf.git /src && \
    cd /src && \
    make && make install && \
    text2pdf /sample.txt | grep -q '%PDF' && \
    apk del --no-cache git build-base && \
    rm -fr /src && rm -f /sample.txt

ENTRYPOINT ["text2pdf"]