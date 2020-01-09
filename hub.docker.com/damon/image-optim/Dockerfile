# damon/img-compress

FROM node

# We need ruby to install the image_optim gems
RUN apt-get update && \
    apt-get install -y ruby && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean -y && \
    apt-get autoremove -y

# https://github.com/toy/image_optim
# https://github.com/toy/image_optim_pack
RUN gem install --no-ri --no-rdoc image_optim image_optim_pack

# svgo
RUN npm install -g svgo

ENTRYPOINT ["image_optim"]
