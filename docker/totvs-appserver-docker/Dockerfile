FROM centos:7

LABEL maintainer "Marcus Sullivan <marcus.sullivan@gmail.com>"

RUN yum -y update \
    && yum -y install \
        dmidecode \
        fontconfig \
        glib2 \
        glibc \
        libstdc++ \
        libuuid \
        wget \
    && rm -rf /var/cache/yum/* \
    && yum clean all

RUN DUMB_INIT_SHA256="37f2c1f0372a45554f1b89924fbb134fc24c3756efaedf11e07f599494e0eff9" \
    && wget -O /usr/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64 \
    && echo "37f2c1f0372a45554f1b89924fbb134fc24c3756efaedf11e07f599494e0eff9 */usr/bin/dumb-init" | sha256sum -c - \
    && chmod +x /usr/bin/dumb-init

ADD 22-07-20-P12_SMARTCLIENT_WEBAPP_6.0.7_LINUX_X86_191205P.TAR.GZ /totvs12/protheus/bin/appserver
ADD 23-04-25-PRINTER_LINUX_X64.TAR.GZ /totvs12/protheus/bin/appserver
ADD 23-06-01-P12_APPSERVER_BUILD-20.3.1.9_LINUX_X64.TAR.GZ /totvs12/protheus/bin/appserver

COPY ./build /build

RUN /build/setup.sh

EXPOSE 9999

VOLUME ["/totvs12/protheus_data", "/totvs12/protheus/apo/"]

WORKDIR /totvs12/protheus/bin/appserver

ENTRYPOINT [ "/usr/bin/dumb-init", "--" ]

CMD [ "/usr/local/bin/my-init.sh" ]
