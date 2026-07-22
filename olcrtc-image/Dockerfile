FROM alpine:3.22

COPY olcrtc-linux-amd64 /usr/local/bin/olcrtc
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /usr/local/bin/olcrtc /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
