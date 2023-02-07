# Python Transformers

Repository to make Dockerfiles available for containers with Huggingface's Transformers. Build your
own Docker Base Image to use Huggingface's Transformers in production.


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
