############################################################
# Dockerfile that replicates a function's y values 
# as network traffic starting at TIMESTART and ending at TIMEEND
############################################################
FROM alpine:latest
LABEL maintainer="walentinlamonos@gmail.com"

# Add curl
RUN apk add curl bc

# TIMESTART and TIMEEND in UNIX time
# TIMESTEP in seconds
# TARGET as IPV4 or FQDN
# FUNCTION has to be a valid function that can be calculated by "bc -l"
# https://www.gnu.org/software/bc/manual/html_chapter/bc_5.html
ENV TIMESTART=0 TIMEEND=2147483647 TIMESTEP=60 TARGET=1.2.3.4 FUNCTION="(-1)*(x-10)^2+100"

RUN { \
    echo '#!/bin/sh'; \
    echo 'mathfunction=$1'; \
    echo 'timestart=$2'; \
    echo 'timeend=$3'; \
    echo 'timestep=$4'; \
    echo 'target=$5'; \
    echo ''; \
    echo '# Wait for initial time'; \
    echo 'while true; do'; \
    echo '  curtime=$(date +%s)'; \
    echo '  if [[ $curtime -ge $timestart ]]; then'; \
    echo '    break'; \
    echo '  fi'; \
    echo '  sleep 1s'; \
    echo 'done'; \
    echo ''; \
    echo 'COUNTER=1'; \
    echo 'curmathfunction=0'; \
    echo 'currentload=0'; \
    echo '# Start hammering away'; \
    echo 'while true; do'; \
    echo '  curtime=$(date +%s)'; \
    echo '  if [[ $curtime -ge $timeend ]]; then'; \
    echo '    break'; \
    echo '  fi'; \
    echo "  curmathfunction=\$(echo \$mathfunction | sed 's/x/'\$COUNTER'/g')"; \
    echo '  currentload=$(echo $curmathfunction | bc -l | cut -f1 -d".")'; \
    echo '  COUNT=0'; \
    echo '  while true; do'; \
    echo '    curl -s "$target" > /dev/null &'; \
    echo '    COUNT=$((COUNT+1))'; \
    echo '    if [[ $COUNT -ge $currentload ]]; then'; \
    echo '      break'; \
    echo '    fi'; \
    echo '  done'; \
    echo '  COUNTER=$((COUNTER+1))'; \
    echo '  sleep $timestep'; \
    echo 'done'; \
} > /root/entry.sh && chmod +x /root/entry.sh

ENTRYPOINT ./root/entry.sh $FUNCTION $TIMESTART $TIMEEND $TIMESTEP $TARGET
