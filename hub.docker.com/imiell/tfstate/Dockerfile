FROM mongo
RUN apt update -y && apt install -y curl net-tools
ADD tfstate /
ADD startup.sh /
CMD /startup.sh
