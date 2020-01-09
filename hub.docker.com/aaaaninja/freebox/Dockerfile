FROM alpine AS prepare_asdf
RUN apk update && apk add git && git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.7.4

FROM ruby AS build-ruby
SHELL ["/bin/bash", "-c"]
COPY --from=prepare_asdf /root/.asdf /root/.asdf
RUN . /root/.asdf/asdf.sh      \
    && asdf plugin-add ruby    \
    && asdf install ruby 2.6.4 \
    && tar caf /asdf_ruby.tar /root/.asdf

FROM python AS build-python
SHELL ["/bin/bash", "-c"]
COPY --from=prepare_asdf /root/.asdf /root/.asdf
RUN . /root/.asdf/asdf.sh        \
    && asdf plugin-add python    \
    && asdf install python 3.7.4 \
    && tar caf /asdf_python.tar /root/.asdf

FROM node AS build-nodejs
SHELL ["/bin/bash", "-c"]
COPY --from=prepare_asdf /root/.asdf /root/.asdf
RUN . /root/.asdf/asdf.sh                                          \
    && asdf plugin-add nodejs                                      \
    && bash ~/.asdf/plugins/nodejs/bin/import-release-team-keyring \
    && asdf install nodejs 12.9.0                                  \
    && tar caf /asdf_nodejs.tar /root/.asdf

FROM golang AS build-golang
SHELL ["/bin/bash", "-c"]
COPY --from=prepare_asdf /root/.asdf /root/.asdf
RUN . /root/.asdf/asdf.sh       \
    && asdf plugin-add golang   \
    && asdf install golang 1.13 \
    && tar caf /asdf_golang.tar /root/.asdf

FROM rust AS build-rust
SHELL ["/bin/bash", "-c"]
COPY --from=prepare_asdf /root/.asdf /root/.asdf
RUN . /root/.asdf/asdf.sh       \
    && asdf plugin-add rust     \
    && asdf install rust 1.37.0 \
    && tar caf /asdf_rust.tar /root/.asdf

FROM node AS build-yarn
SHELL ["/bin/bash", "-c"]
COPY --from=prepare_asdf /root/.asdf /root/.asdf
RUN . /root/.asdf/asdf.sh       \
    && asdf plugin-add yarn     \
    && asdf install yarn 1.17.3 \
    && tar caf /asdf_yarn.tar /root/.asdf

FROM ubuntu
SHELL ["/bin/bash", "-c"]
COPY --from=build-yarn   /asdf_yarn.tar   /
COPY --from=build-nodejs /asdf_nodejs.tar /
COPY --from=build-ruby   /asdf_ruby.tar   /
COPY --from=build-python /asdf_python.tar /
COPY --from=build-golang /asdf_golang.tar /
COPY --from=build-rust   /asdf_rust.tar   /
RUN ls *.tar | xargs -I{} tar xf {} && rm *.tar
