# Dockerfile
FROM ros:jazzy
ARG USERNAME=ros
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Delete user if it exists in container (e.g., Ubuntu Noble: ubuntu)
RUN if id -u $USER_UID ; then userdel $(id -un $USER_UID) ; fi

# Create the user and add sudo support
RUN groupadd --gid $USER_GID $USERNAME && \
    useradd --uid $USER_UID --gid $USER_GID -m $USERNAME && \
    apt-get update && \
    apt-get install -y sudo && \
    echo "$USERNAME ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y python3-pip
RUN apt-get update && apt-get install -y \
    mesa-utils \
    libgl1-mesa-dri \
    x11-apps \
    mc figlet toilet featherpad wget curl \
    ros-jazzy-rviz2 \
    ros-jazzy-py-trees-ros \
    ros-jazzy-py-trees-ros-viewer \
    ros-jazzy-py-trees-ros-tutorials \
    ros-jazzy-rqt \
    ros-jazzy-rqt-image-view \
    python-is-python3

# Set up X11 environment as root
USER root
RUN mkdir -p /tmp/runtime && chmod 700 /tmp/runtime
ENV XDG_RUNTIME_DIR=/tmp/runtime
ENV LIBGL_ALWAYS_SOFTWARE=1
ENV SHELL=/bin/bash

# Revert to default user
USER $USERNAME
CMD ["/bin/bash"]
