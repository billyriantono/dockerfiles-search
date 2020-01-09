FROM python:3.5.8-alpine

# Add image metadata
LABEL org.label-schema.name="Speedtest CLI" \
	org.label-schema.description="Test your network speed from inside a docker container." \ 
	maintainer="Ismail Sunni <imajimatika@gmail.com>"

RUN pip install speedtest-cli

CMD ["speedtest-cli"]
