# Murmur
Super small and easy to setup mumble server.

## Running the server
```bash
docker run --detach --name murmur --publish 64738:64738/tcp --publish 64738:64738/udp hetsh/murmur
```

## Stopping the container
```bash
docker stop murmur
```

## Configuration
Murmur can be configured with a configuration file `/var/lib/murmur/murmur.ini`.
The file must exist, but it can be empty which means murmur uses the default values.

## Creating persistent storage
```bash
DATA="/path/to/data"
mkdir -p "$DATA"
chown -R 1363:1363 "$DATA"
```
`1363` is the numerical id of the user running the server (see Dockerfile).
The user must have RW access to the data directory.
Start the server with the additional mount flags:
```bash
docker run --mount type=bind,source=/path/to/data,target=/var/lib/murmur ...
```

## Automate startup and shutdown via systemd
The systemd unit can be found in my GitHub [repository](https://github.com/Hetsh/docker-murmur).
```bash
systemctl enable murmur --now
```
By default, the systemd service assumes `/apps/murmur` for data and `/etc/localtime` for timezone.
Since this is a personal systemd unit file, you might need to adjust some parameters to suit your setup.

## Fork Me!
This is an open project (visit [GitHub](https://github.com/Hetsh/docker-murmur)). Please feel free to ask questions, file an issue or contribute to it.