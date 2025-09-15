# Base: Ubuntu 22.04
FROM ubuntu:22.04

# Avoid interactive prompts during build
ENV DEBIAN_FRONTEND=noninteractive

ENV USER=root

# Install basic packages, desktop environment, and VNC server
RUN apt-get update && apt-get install -y \
    xfce4 \
    xfce4-goodies \
    tightvncserver \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /root

# Set VNC password
RUN mkdir -p ~/.vnc && \
    echo "123456" | vncpasswd -f > ~/.vnc/passwd && \
    chmod 600 ~/.vnc/passwd

# Create VNC startup script
RUN echo "#!/bin/bash\n\
xrdb $HOME/.Xresources\n\
startxfce4 &" > ~/.vnc/xstartup && chmod +x ~/.vnc/xstartup

# Expose VNC port
EXPOSE 5901

# Start VNC server when container runs
CMD ["bash", "-c", "vncserver :1 -geometry 1280x800 -depth 24 && tail -F /root/.vnc/*.log"]
