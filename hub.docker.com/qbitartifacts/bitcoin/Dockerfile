from debian
env DEBIAN_FRONTEND noninteractive
run apt update && apt install -y wget
run wget https://bitcoincore.org/bin/bitcoin-core-0.17.1/bitcoin-0.17.1-x86_64-linux-gnu.tar.gz -O bitcoin.tgz
run tar xzvf bitcoin.tgz
run cp bitcoin-0.17.1/bin/* /usr/bin/

copy docker-entrypoint.sh /
run chmod +x /docker-entrypoint.sh

cmd ["/docker-entrypoint.sh"]
