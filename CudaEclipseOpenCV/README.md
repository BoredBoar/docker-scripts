make sure docker engine and nvidia-docker are installed

build container with `docker build -t image_name .`

excute container with " nvidia-docker run -it --rm --security-opt seccomp=unconfined -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v \`pwd\`:/data -p 8080:8080 image_name "
