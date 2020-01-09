FROM debian:stretch
MAINTAINER apollo.arkwright@gmail.com

ENV VERSION="8.8.0"

VOLUME ['/opt/nessus']

# 
RUN apt-get update -y && \
	apt-get install -y curl apt-utils net-tools iputils-ping tzdata && \

	# Get the Download ID:
	ID=$(curl -ssl -o - "https://www.tenable.com/downloads/nessus" | tr "," "\n" | grep -B1 "Nessus-8.8.0-debian6_amd64.deb" | awk -F: '/id/ {print $2}' | sort -u | awk 'NF') && \

	# Download the deb package:
	curl -q "https://www.tenable.com/downloads/api/v1/public/pages/nessus/downloads/${ID}/download?i_agree_to_tenable_license_agreement=true" -H "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8" -H "Accept-Language: en-US,en;q=0.5" --compressed -H "Referer: https://www.tenable.com/downloads/nessus" -H "Connection: keep-alive" -H "Upgrade-Insecure-Requests: 1" --output /tmp/nessus.deb && \

	# Install the package:
	apt-get install -f /tmp/nessus.deb && \
	
	# Cleanup:
	rm -rf /tmp/nessus.deb && \
	rm -rf /var/lib/apt/lists/*

EXPOSE 8834

CMD ["/opt/nessus/sbin/nessus-service"]
