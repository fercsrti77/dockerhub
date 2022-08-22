# (c) 2022 Copyright, Real-Time Innovations, Inc. (RTI) All rights reserved.
# RTI grants Licensee a license to use, modify, compile, and create derivative 
# works of the software solely for use with RTI Connext DDS.  Licensee may 
# redistribute copies of the software, provided that all such copies are subject 
# to this license. The software is provided "as is", with no warranty of any 
# type, including any warranty for fitness for any purpose. RTI is under no 
# obligation to maintain or support the software.  RTI shall not be liable for 
# any incidental or consequential damages arising out of the use or inability 
# to use the software.

FROM ubuntu:22.10

#
# Build container:
#   Copy connext installation to this directory
#   $ docker build 
#       --build-arg VERSION=6.1.1 
#       --build-arg ARCH=x64Linux2.6gcc4.4.5 
#       -t routing_service:6.1.1 .
#
# Run container in UDPv4 mode:
#   $ docker run -d 
#       --network host 
#       -v $PWD/license.dat:/rti/license.dat 
#       -e INPUT_DOMAIN=56 
#       -e OUTPUT_DOMAIN=57 
#       --name=routing_service 
#       routing_service:6.1.1
#
# Run container in UDPv4_WAN relay mode:
#   $ docker run -d 
#       -p 16000:16000 
#       -v $PWD/license.dat:/rti/license.dat 
#       -e PUBLIC_ADDRESS=127.0.0.1 
#       -e DOMAIN=56
#       -e PUBLIC_PORT=16000 -e HOST_PORT=16000
#       -e CFG_NAME=Udpv4WanRelayReliable
#       --name=routing_service
#       routing_service:6.1.1
#
# Inspect the image:
#   $ docker run -it rticom/routing_service:6.1.1 /bin/bash
# Start a bash shell:
#   $ docker exec -it routing_service /bin/bash
# See if container is running:
#   $ sudo docker ps -a
# See container logs:
#   $ sudo docker logs routing_service
# Stop container main process:
#   $ docker stop routing_service
# Delete container:
#   $ docker rm  routing_service
# Delete image:
#   $ docker rmi routing_service:6.1.1
#
# Upload to Dockerhub:
#   $ docker login --username <username> --password
#   $ docker image tag routing_service:6.1.1 rticom/routing_service:6.1.1
#   $ docker push rticom/routing_service:6.1.1

# Working directory
ENV CONNEXT_WORK_DIR=/rti
WORKDIR $CONNEXT_WORK_DIR

# Build variables
ARG ARCH=x64Linux2.6gcc4.4.5
ARG VERSION=6.1.1

# Run variables
ENV CONNEXT_VERSION=$VERSION

ENV CONNEXT_ARCH=$ARCH
ENV LD_LIBRARY_PATH $CONNEXT_WORK_DIR/rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH
ENV RTI_LICENSE_FILE="/rti/license.dat"
ENV NDDSHOME=$CONNEXT_WORK_DIR/rti_connext_dds-$CONNEXT_VERSION

# Service configration variables
ENV ARGS=""
ENV INPUT_DOMAIN=1
ENV DOMAIN=1
ENV OUTPUT_DOMAIN=2
ENV ADMIN_DOMAIN=3
ENV MONITORING_DOMAIN=4
ENV PUBLIC_ADDRESS=127.0.0.1
ENV PUBLIC_PORT=16000
ENV HOST_PORT=16000
ENV ADMIN_PUBLIC_PORT=16001
ENV ADMIN_HOST_PORT=16001
ENV MONITORING_PUBLIC_PORT=16002
ENV MONITORING_HOST_PORT=16002
ENV CFG_NAME="DomainBridgingOverLAN"

# Copy image content
COPY routing_service.xml .
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/bin/$CONNEXT_ARCH/rtiroutingserviceapp rti_connext_dds-$CONNEXT_VERSION/resource/app/bin/$CONNEXT_ARCH/rtiroutingserviceapp

COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddscore.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddscore.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddsc.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddsc.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librticonnextmsgc.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librticonnextmsgc.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddsmetp.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddsmetp.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtidlc.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtidlc.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddssecurity.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddssecurity.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtiapputilsc.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtiapputilsc.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtixml2.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtixml2.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtiroutingservice.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtiroutingservice.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtirsinfrastructure.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtirsinfrastructure.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtirsjniadapter.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtirsjniadapter.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddstransporttcp.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libnddstransporttcp.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtimonitoring.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/librtimonitoring.so
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libssl.so.1.1 rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libssl.so.1.1
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libssl.so rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$CONNEXT_ARCH/libssl.so 
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/java/nddsjava.jar rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/java/nddsjava.jar
COPY ./rti_connext_dds-$CONNEXT_VERSION/lib/java/rtiroutingservice.jar rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/java/rtiroutingservice.jar
COPY ./rti_connext_dds-$CONNEXT_VERSION/lib/java/rtirsadapter.jar rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/java/rtirsadapter.jar

# Execute this commend at startup
CMD ./rti_connext_dds-$CONNEXT_VERSION/resource/app/bin/$CONNEXT_ARCH/rtiroutingserviceapp -cfgName $CFG_NAME -cfgFile ./routing_service.xml $ARGS
