FROM alpine:3.5 AS builder
MAINTAINER Davod (Amitie10g) <davidkingnt@gmail.com>

RUN apk -Uu --no-cache add opam make build-base gcc abuild binutils bash ncurses-dev git m4 &&\
  OPAMYES=true opam init && \
  OPAMYES=true opam depext google-drive-ocamlfuse && \
  OPAMYES=true opam install google-drive-ocamlfuse
  
FROM alpine:3.10

RUN apk -Uu --no-cache add libressl2.7-libtls fuse libgmpxx sqlite-libs libcurl ncurses-libs

ENV DRIVE_PATH="/drive"
ENV LABEL="gdrive"

COPY init.sh /
COPY --from=builder /root/.opam/system/bin/google-drive-ocamlfuse /bin/

RUN chmod +x /init.sh
RUN mkdir -p $DRIVE_PATH

CMD ["/init.sh"]
