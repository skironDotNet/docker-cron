FROM alpine:latest

ENV SCHEDULE_EXPR "*/30 * * * *"
ADD job.sh /job.sh
RUN chmod +x /job.sh
RUN apk add --no-cache tini && rm -rf /var/cache/apk/*

ENTRYPOINT ["/sbin/tini", "--"]
CMD echo "$SCHEDULE_EXPR /job.sh" > /crontab.txt && \
/usr/bin/crontab /crontab.txt && rm /crontab.txt && \
/usr/sbin/crond -f
