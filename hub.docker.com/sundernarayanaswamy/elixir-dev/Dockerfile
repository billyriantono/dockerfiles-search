FROM frolvlad/alpine-glibc

MAINTAINER sunder.narayanaswamy@gmail.com

RUN apk update && apk upgrade && apk add build-base \
                      erlang erlang-syntax-tools	\
                      erlang-tools erlang-wx	\
                      erlang-xmerl erlang-parsetools	\
                      erlang-public-key erlang-reltool \
                      erlang-runtime-tools erlang-sasl \
                      erlang-snmp	erlang-ssh \
                      erlang-ssl	erlang-stdlib \	
                      erlang-mnesia erlang-observer \
                      erlang-odbc erlang-orber \
                      erlang-os-mon erlang-otp-mibs \ 
                      erlang-eunit erlang-hipe \
                      erlang-ic erlang-inets	\
                      erlang-jinterface erlang-kernel \
                      erlang-megaco erlang-et \
                      erlang-dialyzer erlang-diameter \	
                      erlang-edoc erlang-eldap \
                      erlang-erl-docgen erlang-erl-interface \
                      erlang-erts erlang-cosevent	\
                      erlang-coseventdomain erlang-cosfiletransfer \
                      erlang-cosnotification erlang-cosproperty \
                      erlang-costime erlang-costransaction \
                      erlang-crypto erlang-debugger \
                      erlang-asn1 erlang-common-test \
                      erlang-compiler erlang-dev \
                      elixir elixir-doc \
                      zsh sudo \
                      emacs-nox \
                      nodejs \
                      the_silver_searcher jq \
                      inotify-tools \
                      git \
                      tree \
                      postgresql-client \
                      zip unzip unrar gzip bzip2 \
                      curl wget \
                      openssh openssh-keygen \
                      aws-cli aws-cli-zsh-completion \
#                     hiawatha \
                      go go-doc go-tools \
                      opam \
                      sqlite \
#                     reason reason-merlin reason-rtop reason-rebuild reason-reactjs \
#                     rust rust-dbg rust-doc cargo cargo-doc cargo-zsh-completion \
                      --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted

RUN npm install -g jshint js-beautify tern \
                   elm elm-format elm-oracle \
      	           bs-platform@3.0.0 reason-cli \
            		   webpack webpack-cli \
                   --unsafe-perm

EXPOSE 4000

WORKDIR /root

CMD /bin/zsh
