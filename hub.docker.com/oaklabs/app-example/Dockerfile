FROM oaklabs/oak:5.0.9

# Create app directory inside the container
WORKDIR /app

# First, we copy just the needed files to do `npm install`. This way our build will not reinstall node modules if we just have changes to our source files
COPY . /app

RUN npm i --engine-strict=true --progress=false --loglevel="error" \
    && npm cache clean --force

# We add an environmental variable that the app looks for to start the app with default url
ENV REMOTE_URL=http://static.oak.host/signage/index.html

# Define the command to run your app using `CMD` which defines your runtime.
CMD ["/app/src/index.js"]