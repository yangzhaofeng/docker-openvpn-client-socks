# OpenVPN-client

This is a docker image of an OpenVPN client tied to a SOCKS proxy server.  It is
useful to isolate network changes (so the host is not affected by the modified
routing).

This supports directory style (where the certificates are not bundled together in one `.ovpn` file) and those that contains `update-resolv-conf`

## Usage

using `docker run` directly:

```bash
docker run -itd \
        --device=/dev/net/tun \
        --restart=always \
        --name=ovpn-socks \
        --cap-add=NET_ADMIN \
        --publish 0.0.0.0:1081:1080 \
        --volume "/srv/docker/ovpn-socks/:/etc/openvpn/:ro" \
        yangzhaofengsteven/openvpn-socks
```

Then connect to SOCKS proxy through through `local.docker:1081`. For example:

```bash
curl --proxy socks5://local.docker:1081 ipinfo.io
```
