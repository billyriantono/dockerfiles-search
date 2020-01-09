FROM paperist/alpine-texlive-ja

RUN apk --no-cache add curl ghostscript && \
    tlmgr update --self && \
    tlmgr install ccicons newtx siunitx stix \
                  pdfcrop
  
WORKDIR /workdir
VOLUME ["/workdir"]
CMD ["sh"]
