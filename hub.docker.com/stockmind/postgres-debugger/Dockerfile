FROM postgres:latest

# Install the postgresql debugger
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    postgresql-$PG_MAJOR-pldebugger