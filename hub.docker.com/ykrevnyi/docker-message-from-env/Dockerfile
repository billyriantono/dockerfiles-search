FROM node:7.10.0

# General configuration
ENV USER app
ENV BASE_DIR /home
ENV APP_NAME api

# Create user
RUN useradd \
    --user-group \
    --create-home \
    --shell /bin/false $USER

WORKDIR /$BASE_DIR/$USER/$APP_NAME

# Copy package.json file
COPY package.json /$BASE_DIR/$USER/$APP_NAME/package.json

RUN npm install -q

USER root
COPY . .

# Set permissions for given user
RUN chmod +x /$BASE_DIR/$USER && \
    chown -R $USER:$USER /$BASE_DIR/$USER

USER $USER
CMD ["npm", "start"]
