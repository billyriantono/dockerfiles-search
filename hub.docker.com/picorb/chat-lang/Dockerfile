FROM correl/erlang

# Install ChicagoBoss
WORKDIR /ChicagoBoss
ADD ./ChicagoBoss /ChicagoBoss
RUN make
WORKDIR /app
ADD ./apalachin /app
ADD boss.config /app/

EXPOSE 		8001

CMD 		["sh", "init-dev.sh"]
