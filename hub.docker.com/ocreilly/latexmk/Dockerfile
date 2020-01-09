FROM paperist/alpine-texlive-ja:latest
RUN tlmgr update --self && \
  tlmgr install sourcecodepro ly1 mweights

LABEL io.whalebrew.name latexmk
ENTRYPOINT ["latexmk"]
CMD [""]
