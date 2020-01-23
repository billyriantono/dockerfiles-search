FROM gilhardl/node

LABEL author="Lucas GILHARD <l.gilhard@gmail.com>"
LABEL description="Docker image for Clever Cloud CLI"

WORKDIR /usr/src/api/

USER root

# CLEVER TOOLS
RUN npm install -g clever-tools

# EXPOSE PORTS
EXPOSE 9005

CMD ["bash"]