FROM alpine:3

RUN apk add --no-cache openjdk17-jre bash libc6-compat gcompat

WORKDIR /opt
COPY trafficparrot-*.zip trafficparrot.zip
RUN unzip trafficparrot.zip && rm trafficparrot.zip && mv trafficparrot-* trafficparrot

RUN chgrp -R 0 /opt/trafficparrot && chmod -R g=u /opt/trafficparrot
ENV LD_LIBRARY_PATH=/usr/lib:/opt/trafficparrot/jre/lib/amd64/server:/opt/trafficparrot/jre/lib/amd64

WORKDIR /opt/trafficparrot
CMD ["./start-foreground.sh"]