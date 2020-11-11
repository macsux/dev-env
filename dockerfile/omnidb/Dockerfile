#FROM alpine:3.11
#FROM busybox:glibc
FROM frolvlad/alpine-glibc
RUN apk add --no-cache bash

# Install Instantclient Basic Light Oracle and Dependencies
#RUN apk --no-cache add libaio libnsl libc6-compat curl && \
RUN apk --no-cache add libaio libnsl curl && \
    cd /tmp && \
    curl -o instantclient-basiclite.zip https://download.oracle.com/otn_software/linux/instantclient/instantclient-basiclite-linuxx64.zip -SL && \
    unzip instantclient-basiclite.zip && \
    mv instantclient*/ /usr/lib/instantclient && \
    rm instantclient-basiclite.zip && \
    ln -s /usr/lib/instantclient/libclntsh.so.19.1 /usr/lib/libclntsh.so && \
    ln -s /usr/lib/instantclient/libocci.so.19.1 /usr/lib/libocci.so && \
    ln -s /usr/lib/instantclient/libociicus.so /usr/lib/libociicus.so && \
    ln -s /usr/lib/instantclient/libnnz19.so /usr/lib/libnnz19.so && \
    ln -s /usr/lib/libnsl.so.2 /usr/lib/libnsl.so.1 && \
    ln -s /lib/libc.so.6 /usr/lib/libresolv.so.2 && \
    ln -s /lib64/ld-linux-x86-64.so.2 /usr/lib/ld-linux-x86-64.so.2

ENV ORACLE_BASE /usr/lib/instantclient
ENV LD_LIBRARY_PATH /usr/lib/instantclient
ENV NLS_LANG AMERICAN_AMERICA.AL32UTF8
ENV TNS_ADMIN /tns_admin/
ENV ORACLE_HOME /usr/lib/instantclient

ENV OMNIDB_VERSION 3.0.2b

RUN apk add --no-cache --virtual .build-deps curl tar \
      && curl -Lo /tmp/omnidb.tar.gz https://github.com/OmniDB/OmniDB/releases/download/3.0.2b/omnidb-server_3.0.2b_linux_x86_64.tar.gz \
      && mkdir /opt/omnidb \
      && tar --strip-components=1 -xzf /tmp/omnidb.tar.gz -C /opt/omnidb \
      && rm -f /tmp/omnidb.tar.gz \
      && mkdir /etc/omnidb \
      && cd /opt/omnidb \
      && find /usr/local -name '*.a' -delete \
      && addgroup -S omnidb && adduser -S omnidb -G omnidb \
      && chown -R omnidb:omnidb /opt/omnidb \
      && chown -R omnidb:omnidb /etc/omnidb

USER omnidb

EXPOSE 8080 25482

WORKDIR /opt/omnidb

ENTRYPOINT ["/opt/omnidb/omnidb-server", "--host=0.0.0.0", "--port=8080", "-d", "/etc/omnidb"]