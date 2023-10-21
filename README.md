# Dockerfile(s) repository

`git` repository to store several `Dockerfile`.

* Getting and running the `docker` images

The easiest way is to grab the `docker` images from Github Container Registry *aka* `ghcr`. For instance,
to run the `teaching` image, you can do

```
docker run --rm -it ghcr.io/xgarrido/dockerfiles/teaching:latest /bin/zsh
```

## Building the image

If you not only want to use the images but also play/change with them then you have to first
checkout this repository
```
git clone https://github.com/xgarrido/dockerfiles
```
and then run the next command from your local repository
```
cd teaching
docker build -t teaching:latest .
```

You can also build the `docker` image without checking out the github repository by doing
```
docker build -t teaching:latest "github.com/xgarrido/dockerfiles#:teaching"
```

The `-t` flag set the name of the image and will be used when running your container.

Every time you use the `build` command, `docker` uses a cached version to decrease the start
time. If you want to restart from scratch (for instance to update a remote git repository within
your `docker` image), you should use the `--no-cache` option in the `docker build` command line. All
the options of `docker build` command can be found
[here](https://docs.docker.com/engine/reference/commandline/build).

* Running the image

Given that the `build` operation succeeds, you can interactively run your image by doing
```
docker run --rm -it teaching:latest /bin/zsh
```
You will be prompted as `teaching` user to a `zsh` terminal. The `--rm` ensures everything gets cleaned
when stopping the image.

To forward `DISPLAY`, you should frist allow `docker` to do it
```
xhost +local:docker
```
and then you should add the following options to the `docker run` command
```
docker run -e DISPLAY`$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    --rm -it teaching:latest /bin/zsh
```
