#
# Dockerfile to create a Node.js image
#
# This Dockerfile makes the following assumptions:
# - The collectives enabling scripts (joinMember, removeMember) will be placed in
#   /opt/ibm/docker in the Docker container
# - Node.js servers are created at /root/wlpn
# - The Node.js server will be "defaultServer" (for example, /root/wlpn/defaultServer)
# - The application to install will already have its dependencies resolved by "npm install"
# - The Docker container will be run using --net=host, so that no ports are explicitly exported in this file

FROM node:4.7.3
#
# Auto-start the Node.js server with the container
#
ENTRYPOINT ["/usr/local/bin/wlpn-server", "run", "defaultServer"]
# Set environment variable
# ENV DEBUG=wlpn-cli*
# Add collectives enabling scripts
#
ADD joinMember /opt/ibm/docker/
RUN chmod +x /opt/ibm/docker/joinMember
ADD removeMember /opt/ibm/docker/
RUN chmod +x /opt/ibm/docker/removeMember
#
# Update the OS and JRE
#
RUN apt-get update
#
# Install APIConnect collective member
#
RUN npm install -g apiconnect-collective-member
#
# Use the code below to install an application for use onto the Docker image
#
COPY notes-1.0.0.tgz /root/wlpn/
RUN wlpn-server unpack defaultServer /root/wlpn/notes-1.0.0.tgz
