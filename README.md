Rust source-to-image
====================

This repository contains the source for building Rust applications as reproducible Docker images using [source-to-image](https://github.com/openshift/source-to-image).

For more information about using these images with OpenShift, please see the
official [OpenShift Documentation](https://docs.openshift.org/latest/architecture/core_concepts/builds_and_image_streams.html#source-build).

Installation
---------------
You will either need to pre-install [docker-squash](https://github.com/goldmann/docker-squash) that is used for squashing docker layers
or you can skip squashing with `export SKIP_SQUASH=1`.

To prepare the builder image:
```shell
$ git clone https://github.com/openshift-s2i/s2i-rust.git
$ cd s2i-rust
$ make build
```

Use
---------------
Use the `s2i` tool to build the final image that contains your application code:
```shell
$ s2i build ./examples/test-app/ openshift/rust-132-centos7 rust-test-app
```
* `./1.32/test/test-app/` is the top directory of your source code.
* `openshift/rust-132-centos7` is the name of the builder image created by `make build` above.
* `rust-test-app` is the name of the new image that contains your application code.

Finally, run the image:
```shell
$ docker run rust-test-app
```

Environment variables
---------------------

Application developers can use the following environment variables to configure the runtime behavior of this image:

NAME        | Description
------------|-------------
PROXY       | Use a cargo proxy during assembly

Versions
---------------
Rust versions currently supported:
* 1.7
* 1.20
* 1.26
* 1.32