# Python Transformers

Repository to make Dockerfiles available for containers with Huggingface's Transformers. Build your
own Docker Base Image to use Huggingface's Transformers in production.

Some images are avalable at [Docker Hub](https://hub.docker.com/r/rodrigocaus/python-transformers). You can also build
your own image to fill your purposes. 

## Building

Run `docker build` with build args to manage transformers installation.

### Transformers and PyTorch (CPU)

Specify `PYTHON_BASE_TAG` (from [official Python Docker Image](https://hub.docker.com/_/python/)) and
`TRANSFORMERS_VERSION` (using [Pip version identification](https://peps.python.org/pep-0440/)). One can
also specify `EXTRA_PACKAGES` to be installed with `transformers[torch]`:

```bash
$ export PYTHON_TAG=3.9-slim
$ export VERSION="==4.26"
$ docker build -t python-transformers \
    --build-arg PYTHON_BASE_TAG=$PYTHON_TAG \
    --build-arg TRANSFORMERS_VERSION=$VERSION \
    --build-arg EXTRA_PACKAGES="torchvision torchaudio" \
    -f Dockerfile.torch-cpu .
```

### Transformers and PyTorch (GPU)

This image uses an official [nvidia/cuda](https://hub.docker.com/r/nvidia/cuda) container as base image.
Specify `PYTHON_VERSION` and
`TRANSFORMERS_VERSION` (using [Pip version identification](https://peps.python.org/pep-0440/)). One can
also specify `EXTRA_PACKAGES` to be installed with `transformers[torch]`:

```bash
$ export PYTHON_VERSION=3.10
$ export VERSION="~=4.26"
$ docker build -t python-transformers \
    --build-arg PYTHON_VERSION=$PYTHON_VERSION \
    --build-arg TRANSFORMERS_VERSION=$VERSION \
    --build-arg EXTRA_PACKAGES="torchvision torchaudio" \
    -f Dockerfile.torch-gpu .
```
