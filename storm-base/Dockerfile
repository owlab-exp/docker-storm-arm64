FROM owlab/oracle-jdk8-arm64

MAINTAINER Hun Jae Lee <hunjae.lee@gmail.com>

ENV STORM_VERSION 0.10.0
ENV STORM_HOME /opt/storm

RUN apt-get update && apt-get install -y --no-install-recommends openssh-server supervisor wget \
	&& rm -rf /var/lib/apt/lists/* \
	&& echo 'root:admin' | chpasswd \
	&& sed -i 's/^PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
	&& wget -q -O - http://mirror.apache-kr.org/storm/apache-storm-${STORM_VERSION}/apache-storm-${STORM_VERSION}.tar.gz | tar zxvf - -C /opt \
    	&& ln -s /opt/apache-storm-${STORM_VERSION} /opt/storm \
	&& apt-get remove -y wget && rm -rf /var/lib/apt/lists/* \
# add storm user and group
	&& groupadd storm; useradd --gid storm --home-dir /home/storm --create-home --shell /bin/bash storm; chown -R storm:storm /opt/apache-storm-${STORM_VERSION} \
# make directory for storm logs
	&& mkdir -p /logs; chown -R storm:storm /logs 

COPY storm.yaml ${STORM_HOME}/conf/storm.yaml
COPY cluster.xml ${STORM_HOME}/log4j2/cluster.xml
COPY worker.xml ${STORM_HOME}/log4j2/worker.xml
COPY config-supervisord.sh /usr/bin/config-supervisord.sh
COPY start-supervisor.sh /usr/bin/start-supervisor.sh

RUN chmod 755 /usr/bin/config-supervisord.sh /usr/bin/start-supervisor.sh \
# change supervisord.conf to run supervisor foreground
	&&  sed -i 's/\[supervisord\]/[supervisord]\nnodaemon=true/' /etc/supervisor/supervisord.conf \
# change supervisord.conf to lay log file in the logs directory
	&& sed -i 's/\/var\/log/\/logs/' /etc/supervisor/supervisord.conf

EXPOSE 22
VOLUME ["/logs"]
