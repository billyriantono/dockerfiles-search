FROM cypress/included:3.4.1

COPY check.js /opt/resource/check
COPY in.js /opt/resource/in
COPY out.js /opt/resource/out

RUN chmod +x /opt/resource/out /opt/resource/in /opt/resource/check

WORKDIR /opt/resource