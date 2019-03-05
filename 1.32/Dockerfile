FROM openshift/base-centos7

# This image provides a Rust environment you can use to run your Rust
# applications.

EXPOSE 8080

ENV RUST_VERSION 1.32

LABEL io.k8s.description="Platform for building and running Rust 1.32 applications" \
      io.k8s.display-name="Rust 1.32" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,rust,rust132"

RUN yum install -y epel-release && \
    INSTALL_PKGS="rust-1.32.0 cargo-1.32.0" && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

# Copy the S2I scripts from the specific language image to $STI_SCRIPTS_PATH
COPY ./s2i/bin/ $STI_SCRIPTS_PATH

USER 1001

# Set the default CMD to print the usage of the language image
CMD $STI_SCRIPTS_PATH/usage

