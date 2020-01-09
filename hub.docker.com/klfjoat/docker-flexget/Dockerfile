FROM python:3.5-alpine

# Run update and installs.
# Pin setuptools to 32 to avoid current race condition https://github.com/pypa/setuptools/issues/951
RUN apk add --update                        \
 && pip install --upgrade pip               \
 && pip install --upgrade setuptools==32    \
 && pip install --upgrade flexget~=2.10.0   \
                          transmissionrpc

# Expose the WebUI port
EXPOSE 5050/tcp

# Define volumes
VOLUME /config

# Default command
# Reference: https://flexget.com/CLI
# Set the config file TODO: make this a variable controllable in FreeNAS
# Set the log level to VERBOSE so that the log file will have info.
# TODO: Find out how to expose this as the log file to FreeNAS
# Start the daemon.
# Use --autoreload-config to force config reloads before task execution.
CMD ["flexget", "-c", "/config/config.yml", "--loglevel", "verbose", "daemon", "start", "--autoreload-config"]
