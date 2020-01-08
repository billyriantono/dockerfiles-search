# mssql-agent-fts-ha-tools
# Maintainers: Microsoft Corporation (twright-msft on GitHub)
# GitRepo: https://github.com/Microsoft/mssql-docker

FROM  ubuntu:16.04
ENV ACCEPT_EULA=Y
ENV MSSQL_SA_PASSWORD=<1qazXSW@>
ENV MSSQL_RPC_PORT=135
ENV MSSQL_DTC_TCP_PORT=51000

#Install curl since it is needed to get repo config
# Get official Microsoft repository configuration
#RUN export DEBIAN_FRONTEND=noninteractive && \
#    apt-get install -y curl apt-transport-https && \
RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -yq curl apt-transport-https && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list | tee /etc/apt/sources.list.d/mssql-server.list && \
    apt-get update && \

    # Install SQL Server from apt
    apt-get install -y mssql-server && \
    # Install optional packages
    apt-get install -y mssql-server-fts && \
    apt-get update && \
    # Cleanup the Dockerfile
    apt-get clean && \
    rm -rf /var/lib/apt/lists
# Install SQL Server which a prerequisite for the optional packages below.
# Install optional packages.  Comment out the ones you don't need
#RUN apt-get update && \
#    apt-get install -y mssql-server mssql-server-ha mssql-server-fts mssql-tools 

# Run SQL Server process
CMD /opt/mssql/bin/sqlservr
