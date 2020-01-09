FROM mcr.microsoft.com/mssql/server:2017-CU14

LABEL maintainer='Glenn Mattheij'

ENV ACCEPT_EULA=Y
ENV SA_PASSWORD=Hopjesvla123
ENV MSSQL_PID=Express
EXPOSE 1433/tcp

RUN /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
# As the setting above does not work, let's use the workaround below
RUN echo 127.0.0.1 settings-win.data.microsoft.com >> /etc/hosts
RUN echo 127.0.0.1 vortex.data.microsoft.com >> /etc/hosts

CMD /opt/mssql/bin/sqlservr
