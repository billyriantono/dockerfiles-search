FROM python:3.4-alpine3.8

# download curl
RUN apk add --no-cache curl

# download speedtest python script
RUN curl https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py --output /speedtest.py

# run it on container start
CMD echo "!!!!STARTING SPEED TEST!!!!" ; python /speedtest.py ; echo "!!!!SPEED TEST FINISHED!!!!" ;
