# Eclipse Mosquitto Docker Image

## Volumes

Three docker volumes have been created in the image to be used for configuration, persistent storage, and logs.

```bash
/app/config
/app/data
/app/log
```

## User/Group

The image runs mosquitto under the mosquitto user and group, which are created
with a uid and gid of 1883.

## Configuration

When creating a container from the image, the default configuration values are used.
To use a custom configuration file, mount a **local** configuration file to `/app/config/mosquitto.conf`

```bash
docker run -it -p 1883:1883 -v <absolute-path-to-configuration-file>:/mosquitto/config/mosquitto.conf eclipse-mosquitto:<version>
```

:boom: if the mosquitto configuration (mosquitto.conf) was modified
to use non-default ports, the docker run command will need to be updated
to expose the ports that have been configured, for example:

```bash
docker run -it -p 1883:1883 -p 8080:8080 -v <absolute-path-to-configuration-file>:/mosquitto/config/mosquitto.conf eclipse-mosquitto:<version>
```

Configuration can be changed to:

* persist data to `/app/data`
* log to `/app/log/mosquitto.log`

i.e. add the following to `mosquitto.conf`:

```
persistence true
persistence_location /mosquitto/data/

log_dest file /mosquitto/log/mosquitto.log
```

**Note**: For any volume used, the data will be persistent between containers.