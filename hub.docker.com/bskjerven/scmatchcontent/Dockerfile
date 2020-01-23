FROM library/python:3.3

RUN apt-get update && apt-get -y install iproute2 net-tools ethtool nano dnsutils

CMD ["/usr/bin/python", "-m", "SimpleHTTPServer", "5000"]
