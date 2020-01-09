FROM python

#Set API key
ENV AUTH_KEY = ""

# Install odrive Sync Agent & make odrive folder
RUN od="$HOME/.odrive-agent/bin" && curl -L "https://dl.odrive.com/odrive-py" --create-dirs -o "$od/odrive.py" && curl -L "https://dl.odrive.com/odriveagent-lnx-64" | tar -xvzf- -C "$od/" && curl -L "https://dl.odrive.com/odrivecli-lnx-64" | tar -xvzf- -C "$od/" && mkdir /odrive

COPY start_odrive.sh /root/.odrive-agent/bin
RUN chmod +x /root/.odrive-agent/bin/start_odrive.sh

# Run the odrive Sync Agent server in the background
#ENTRYPOINT nohup "$HOME/.odrive-agent/bin/odriveagent">/dev/null
#ENTRYPOINT /root/.odrive-agent/bin/start_odrive.sh
ENTRYPOINT /bin/bash
