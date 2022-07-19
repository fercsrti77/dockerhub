FROM ubuntu:20.04

# Copy connext installation to this directory
# Copy license file to this directory with name license.dat
#
# Build container:
#   $ docker build --build-arg VERSION=6.1.1 --build-arg IS_ARCH=x64Linux2.6gcc4.4.5 -t routing_service:6.1.1 .
# Run container in UDPv4 mode:
#   $ docker run -d 
#       --network host 
#       -v $PWD/license.dat:/connext/license.dat 
#       -e INPUT_DOMAIN=56 
#       -e OUTPUT_DOMAIN=57 
#       --name=routing_service 
#       routing_service:6.1.1
# Run container in UDPv4_WAN relay mode:
#   $ docker run -d 
#       -p 16000:16000 
#       -v $PWD/license.dat:/connext/license.dat 
#       -e PUBLIC_ADDRESS=127.0.0.1 
#       -e "DOMAIN=56"
#       -e "PUBLIC_PORT=16000" -e "HOST_PORT=16000"
#       -e "CFG_NAME=Udpv4WanRelayReliable"
#       --name=routing_service
#       routing_service:6.1.1
# Start a bash shell:
#   $ docker exec -it routing_service bash
# Stop container main process:
#   $ docker stop routing_service
# Delete container:
#   $ docker rm  routing_service
# Delete image:
#   $ docker rmi routing_service:6.1.1
#
# Upload to Dockerhub:
#   $ docker login <username>
#   $ docker image tag routing_service:6.1.1 <username>/routing_service:6.1.1
#   $ docker push <username>/routing_service:6.1.1

#Working directory
WORKDIR /connext

#Build variables
ARG VERSION=6.1.1
ARG IS_ARCH=x64Linux2.6gcc4.4.5

#Run variables
ENV LD_LIBRARY_PATH $WORKDIR/rti_connext_dds-$CONNEXT_VERSION
ENV ARGS=""
ENV RTI_LICENSE_FILE="/connext/license.dat"
ENV CONNEXT_VERSION=$VERSION
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
ENV CFG_NAME="Udpv4ToUdpv4TwoDomainReliable"

#Copy image content
COPY routing_service.xml .
COPY ./rti_connext_dds-$CONNEXT_VERSION/bin/rtiroutingservice rti_connext_dds-$CONNEXT_VERSION/bin/rtiroutingservice
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/bin/$IS_ARCH/rtiroutingserviceapp rti_connext_dds-$CONNEXT_VERSION/resource/app/bin/$IS_ARCH/rtiroutingserviceapp
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$IS_ARCH/* rti_connext_dds-$CONNEXT_VERSION/resource/app/lib/$IS_ARCH/
COPY ./rti_connext_dds-$CONNEXT_VERSION/resource/scripts/* rti_connext_dds-$CONNEXT_VERSION/resource/scripts/

# Execute this commend at startup
CMD ./rti_connext_dds-$CONNEXT_VERSION/bin/rtiroutingservice -cfgName $CFG_NAME -cfgFile ./routing_service.xml $ARGS

