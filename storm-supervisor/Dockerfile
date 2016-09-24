FROM owlab/storm-base-arm64:0.10.0

MAINTAINER Hun Jae Lee <hunjae.lee@gmail.com>

RUN mkdir /etc/supervisor.d
COPY sshd.supervisord.conf /etc/supervisor.d/sshd.supervisord.conf
RUN cat /etc/supervisor.d/sshd.supervisord.conf >> /etc/supervisor/supervisord.conf

# worker ports
EXPOSE 6700 6701 6702 6703
# log viewer
EXPOSE 8000
# for ssh
EXPOSE 22

RUN /usr/bin/config-supervisord.sh supervisor
RUN /usr/bin/config-supervisord.sh logviewer

CMD ["/usr/bin/start-supervisor.sh"]
