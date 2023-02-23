[![!Docker Pulls](https://img.shields.io/docker/pulls/pombeirp/pihole-dote.svg?color=green&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=pulls&logo=docker)](https://hub.docker.com/r/pombeirp/pihole-dote)

This Docker image builds on the [official Pi-hole Docker image from pi-hole.net](https://hub.docker.com/r/pihole/pihole),
and packs it with the [DoTe executable](https://github.com/chrisstaite/DoTe/releases) from
https://github.com/chrisstaite/DoTe. This has 2 advantages:

- reduces the space required in the UDM Pro to build the image layers;
- simplifies the [UDM quickstart](https://github.com/chrisstaite/DoTe#quick-start-for-udmp) to:

  ```shell
  #!/bin/sh

  podman pull pombeirp/pihole-dote:2023.02.2
  podman stop pihole
  podman rm pihole
  podman run -d --network dns --restart always \
      --name pihole \
      -e TZ="Europe/London" \
      -v "/data/etc-pihole/:/etc/pihole/" \
      -v "/data/pihole/etc-dnsmasq.d/:/etc/dnsmasq.d/" \
      --dns=127.0.0.1 \
      --hostname pi.hole \
      -e DOTE_OPTS="-s 127.0.0.1:5053" \
      -e VIRTUAL_HOST="pi.hole" \
      -e PROXY_LOCATION="pi.hole" \
      -e PIHOLE_DNS_="127.0.0.1#5053" \
      -e ServerIP="10.0.5.3" \
      -e IPv6="True" \
      pombeirp/pihole-dote:2023.02.2
  ```

> Tested on a UniFi Dream Machine Pro with UniFi OS 2.4.27.

The source code for this image is at [GitHub](https://github.com/pedropombeiro/pi-hole-dote).
