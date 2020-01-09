FROM sameersbn/squid
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt install -y net-tools && apt-get install -y openconnect
COPY password.txt .
