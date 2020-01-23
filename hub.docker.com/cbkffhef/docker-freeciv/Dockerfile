from        debian:stretch-slim
maintainer  Christian Becker-Kapraun "cbk@freifunk-hennef.de"
run     apt-get update && apt-get install -y wget freeciv-server
run	useradd freeciv
user    freeciv
entrypoint ["/usr/games/freeciv-server"]
cmd ["--saves", "/freeciv", "--port", "53773" ]
expose 53773
