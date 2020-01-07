FROM node:6.4.0

# Add rootless user
# RUN groupadd -r cassandrasource && useradd -r -g cassandrasource cassandrasource

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

EXPOSE 3000
# USER cassandrasource
ENTRYPOINT ["./entry.sh"]

