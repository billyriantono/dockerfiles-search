FROM truemath/osrm-ubuntu:latest

MAINTAINER Christophe Van Huele <cvh@solvice.io>


# Set the entrypoint
COPY docker-entrypoint.sh /
COPY truck.lua /osrm-profiles/truck.lua
COPY car2.lua /osrm-profiles/car2.lua

RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5000
