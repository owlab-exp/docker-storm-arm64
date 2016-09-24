From owlab/storm-base-arm64:0.10.0

MAINTAINER Hun Jae Lee <hunjae.lee@gmail.com>

RUN /usr/bin/config-supervisord.sh nimbus
RUN /usr/bin/config-supervisord.sh drpc

# nimbus.thrift.port
EXPOSE 6627
# drpc.port
EXPOSE 3772
# drpc.invocation.port
EXPOSE 3773

CMD ["/usr/bin/start-supervisor.sh"]
