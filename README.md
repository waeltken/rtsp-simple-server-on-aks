# Continous Video Streaming to Azure Storage Account

This is based on the [RTSP Simple Server](https://github.com/aler9/rtsp-simple-server).

Use a Docker image with ffmpeg included. Meaning you have to build your own version of the simple server. `./Dockerfile`

http://pendelcam.kip.uni-heidelberg.de/mjpg/video.mjpg

rtsp://wowzaec2demo.streamlock.net/vod/mp4:BigBuckBunny_115k.mp4

```shell
docker build -t rtsp-simple-server .
docker run --rm -it --network=host --name ava -v $PWD/rtsp-simple-server.yaml:/rtsp-simple-server.yml:ro -v $PWD/output:/output rtsp-simple-server
ffmpeg -re -stream_loop -1 -i sample-video.mkv -c copy -f rtsp rtsp://localhost:8554/sample
```

# Todos:

[Replace streams volumeMount with Azure File Share](https://docs.microsoft.com/en-us/azure/aks/azure-files-dynamic-pv)
