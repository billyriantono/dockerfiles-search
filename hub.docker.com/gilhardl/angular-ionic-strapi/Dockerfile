ARG NODE_VERSION=10.15
FROM gilhardl/node:$NODE_VERSION

LABEL author="Lucas GILHARD <l.gilhard@gmail.com>" description="Docker image for Angular development"

USER root

# ANGULAR x IONIC x STRAPI
RUN npm install -g @angular/cli ionic strapi@alpha

WORKDIR /usr/src/app/

# EXPOSE PORTS
EXPOSE 4200 49153 8100 1337

CMD ["bash"]