FROM hpccsystems/hpcc-base:7-xenial

RUN apt-get update
RUN apt-get install -y python3.5 ansible curl iputils-ping
RUN ln -s /usr/bin/python3.5 /usr/bin/python3


RUN groupadd hpcc && useradd -s /bin/bash -r -m -d /home/hpcc -g hpcc -c "hpcc Runtime User" hpcc

ENV VERSION 7.0.14
ENV FULL_VERSION 7.0.14-1
#ENV PLATFORM_DOWNLOAD_MD5  a62b43a1ef1ecf7d8d702d9033e9cf39
ENV PLATFORM_PACKAGE hpccsystems-platform-community_${FULL_VERSION}xenial_amd64.deb

RUN set -x \
   #&&  wget  "http://wpc.423a.rhocdn.net/00423A/releases/CE-Candidate-${VERSION}/bin/platform/${PLATFORM_PACKAGE}" \
   && wget "http://10.240.32.242/builds/custom/JIRA/HPCC-20619/${PLATFORM_PACKAGE}" \
   #&& echo "$PLATFORM_DOWNLOAD_MD5 ${PLATFORM_PACKAGE}" | md5sum -c - \
   && dpkg -i "${PLATFORM_PACKAGE}" \
   && rm -rf "${PLATFORM_PACKAGE}"

EXPOSE 8010 8002 8015 9876

RUN cp -r /home/hpcc/.ssh ~/
COPY hpcc-tools /opt/hpcc-tools
COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["/usr/sbin/sshd", "-D"]
