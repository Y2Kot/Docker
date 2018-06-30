# Docker
Dockerfiles for Radio suites based on LimeSDR

#To start BaseSuite enter:
sudo docker run -v /dev/bus/usb:/dev/bus/usb --privileged -it limebase

#To start OsmoBTS enter:
1. sudo docker run --name="YOUR_CONTAINER_NAME" --device=/dev/bus/usb/XXX/XXX -itd y2kot/limeosmonitb
2. sudo docker exec -it mts bash -c ./startBTS
