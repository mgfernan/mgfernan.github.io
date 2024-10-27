FROM debian:12.7-slim



RUN apt update \
 && apt install -y wget python3 python3-pip \
 && python3 -m pip config set global.break-system-packages true \
 && python3 -m pip install jupyter matplotlib plotly \
 && wget -O /tmp/quarto.deb https://github.com/quarto-dev/quarto-cli/releases/download/v1.5.57/quarto-1.5.57-linux-amd64.deb \
 && dpkg -i /tmp/quarto.deb \
 && rm /tmp/quarto.deb
