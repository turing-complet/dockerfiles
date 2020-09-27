# Run xeyes in a container
#
# docker run -d \
#-v /tmp/.X11-unix:/tmp/.X11-unix \
#-e DISPLAY=unix$DISPLAY \
#--device /dev/dri:/dev/dri \
#--name xeyes \
#xeyes:latest
#

FROM ubuntu:bionic
RUN apt-get update
RUN apt-get install -y x11-apps
CMD ["xeyes"]
