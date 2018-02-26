# docker-asterisk

## What is it based on?

Generally this is based on:
* Centos 7 base images
* Latest current available version of Asterisk certified branch (for LTS releases)

## Running it.

Asterisk with SIP tends to use a wide range of UDP ports (for RTP), so we have chosen to run the main aster container with `--net=host` option. We can now expose a range of ports with `--expose=10000-20000`, however, it [can be very slow for a large number of ports](https://github.com/docker/docker/issues/14288).

# Run the main asterisk container.
docker run \
    --name $NAME_ASTERISK \
    -v $(pwd)/conf/:/etc/asterisk/ \
    --net=host \
    -d -t michaelkrog/asterisk
```

## Building it.

Just issue, with your current-working-dir as the clone:

```bash
docker build -t michaelkrog/asterisk .
```


## Lessons Learned

* I needed to disable the `BUILD_NATIVE` compiler flag. Without asterisk would throw an `illegal instruction` when run in a new place.
  * [This stackexchange answer helped](http://stackoverflow.com/questions/19607378/illegal-instruction-error-comes-when-i-start-asterisk-1-8-22). Thanks arheops
  * Also this note [about Asterisk 11 release](https://wiki.asterisk.org/wiki/display/AST/New+in+11) provides some reference, too.