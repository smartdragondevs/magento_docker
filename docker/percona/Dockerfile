FROM centos:7
MAINTAINER Percona Development <info@percona.com>

RUN yum install -y http://www.percona.com/downloads/percona-release/redhat/0.1-6/percona-release-0.1-6.noarch.rpm
RUN yum install -y epel-release

RUN yum install --enablerepo=percona-experimental* -y Percona-Server-server-80 Percona-Server-tokudb-80 Percona-Server-rocksdb-80 jemalloc which policycoreutils  \
    && rm -rf /var/cache/yum \
    && yum clean all \
    && /usr/bin/install -m0640 -omysql -gmysql /dev/null /etc/sysconfig/mysql \
    && mkdir /docker-entrypoint-initdb.d

RUN echo "LD_PRELOAD=/usr/lib64/libjemalloc.so.1" >> /etc/sysconfig/mysql
RUN echo "THP_SETTING=never" >> /etc/sysconfig/mysql


VOLUME /var/lib/mysql

COPY ps-entry.sh /ps-entry.sh

ENTRYPOINT ["/ps-entry.sh"]

EXPOSE 3306 33060

USER mysql

CMD ["mysqld"]