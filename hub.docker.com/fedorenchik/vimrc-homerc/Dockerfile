FROM thinca/vim:latest as builder

RUN apk add --update git \
&& git clone --depth 1 https://github.com/fedorenchik/homerc.git


FROM thinca/vim:latest

LABEL maintainer="Leonid V. Fedorenchik <leonid@fedorenchik.com>"

COPY --from=builder /root/homerc/.vim /root/.vim/
COPY --from=builder /root/homerc/.vimrc /root/

WORKDIR /root

ENTRYPOINT ["/usr/local/bin/vim"]
