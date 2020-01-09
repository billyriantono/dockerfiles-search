FROM python:3.7
LABEL MAINTAINER Jostein Austvik Jacobsen <jostein@nlb.no> <http://www.nlb.no/>

# Create app directory
WORKDIR /usr/src/app

# Install dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt

# Install application
COPY src/ ./

# expose the default HTTP port
EXPOSE 80

# Run tests
RUN [ "python", "run.py", "test" ]

HEALTHCHECK --interval=10s --timeout=10s --start-period=10s CMD http_proxy="" https_proxy="" curl --fail http://${HOST-0.0.0.0}:${PORT:-80}/statuspage/v1/health/ || exit 1
CMD [ "python", "run.py" ]
