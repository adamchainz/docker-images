FROM circleci-fullstack

USER root

# Install deps to download and install Chrome and then clean up after ourselves
RUN apt-get update &&  \
    apt-get install -y --no-install-recommends xvfb ffmpeg libgconf-2-4 && \
    curl -o /tmp/google-chrome-stable_current_amd64.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    apt install -y --no-install-recommends /tmp/google-chrome-stable_current_amd64.deb && \
    rm /tmp/google-chrome-stable_current_amd64.deb && \
    apt-get clean -y && \
    apt-get autoremove --purge -y && \
    rm -rf /var/lib/apt/lists/* /var/tmp/* /tmp/*

# Ensure python3.6 is default
RUN update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.7 10 && \
    update-alternatives --install /usr/bin/python python /usr/local/bin/python3.7 10

# Setup Xvfb
RUN echo DISPLAY=":99" >> /etc/environment
COPY xvfb.init /etc/init.d/xvfb
RUN chmod +x /etc/init.d/xvfb

# Following line fixes https://github.com/SeleniumHQ/docker-selenium/issues/87
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null

USER ciuser
