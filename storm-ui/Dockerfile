FROM owlab/storm-base-arm64:0.10.0

MAINTAINER Hun Jae Lee <hunjae.lee@gmail.com>

# web interface
EXPOSE 8080

RUN /usr/bin/config-supervisord.sh ui

CMD ["/usr/bin/start-supervisor.sh"]
