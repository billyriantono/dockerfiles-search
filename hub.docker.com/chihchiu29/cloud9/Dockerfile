FROM kdelfour/cloud9-docker:latest

MAINTAINER Chih Chiu <chih.chiu.19@gmail.com>

# Config/Environment setup.
COPY data/dot_c9_user_settings /root/.c9/user.settings

# ------------------------------------------------------------------------------
# Expose ports.
EXPOSE 80
EXPOSE 3000

# ------------------------------------------------------------------------------
# Start supervisor, define default command.
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
