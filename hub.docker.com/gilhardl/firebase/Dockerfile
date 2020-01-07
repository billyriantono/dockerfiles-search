FROM gilhardl/node

LABEL author="Lucas GILHARD <l.gilhard@gmail.com>"
LABEL description="Docker image for Firebase CLI"

WORKDIR /usr/src/app/

USER root

# FIREBASE
RUN npm install -g firebase-tools

# EXPOSE PORTS
EXPOSE 9005

CMD ["bash"]