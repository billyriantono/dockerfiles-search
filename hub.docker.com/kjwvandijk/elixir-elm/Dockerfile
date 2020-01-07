FROM kjwvandijk/elixir-elm:elixir

LABEL maintainer="Koen van Dijk <kjw.vandijk@gmail.com>"

# update the repository sources list
# and install dependencies
RUN apt-get update \
    && apt-get install -y curl git \
    && apt-get -y autoclean

ENV PATH="${PATH}:/root/.asdf/shims:/usr/lib/asdf/bin"
ENV NODE_VERSION 12.13.1
ENV ELM_VERSION 0.19.1


RUN git clone https://github.com/asdf-vm/asdf.git /usr/lib/asdf --branch v0.7.5 && \
    echo -e '\n. /usr/lib/asdf/asdf.sh' >> ~/.bashrc && \
    echo -e '\n. /usr/lib/asdf/completions/asdf.bash' >> ~/.bashrc 

RUN asdf plugin-add nodejs https://github.com/asdf-vm/asdf-nodejs.git && \
    bash ~/.asdf/plugins/nodejs/bin/import-release-team-keyring && \
    asdf install nodejs $NODE_VERSION && \
    asdf global nodejs $NODE_VERSION 

RUN asdf plugin-add elm && \
    asdf install elm $ELM_VERSION && \
    asdf global elm $ELM_VERSION

CMD [ "/bin/bash" ]