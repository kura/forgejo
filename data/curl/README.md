# Testing

## curl

### Automatic ECH
```
$ docker run --rm git.kura.gg/kura/forgejo/curl \
    -H "User-Agent: Mozilla/5.0" \
    -v \
    --http3 \
    --tlsv1.3 \
    --ech true \
    https://git.kura.gg

... snip ...
* ECH: ECHConfig from DoH HTTPS RR
* ECH: imported ECHConfigList of length 64
... snip ...
```

### Manual ECH

```
$ dig +short HTTPS git.kura.gg
1 . alpn="h3" ipv4hint="46.62.173.123" ech="AD7+DQA6WQAgACCVicJ2w8tUedISATcF6ThvruDbAfRKmuZTT+B5oyQGWgAEAAEAAQALZ2l0Lmt1cmEuZ2cAAA==" ipv6hint="2a01:4f9:c013:f9a1::1"


$ docker run --rm git.kura.gg/kura/forgejo/curl \
    -H "User-Agent: Mozilla/5.0" \
    -v \
    --http3 \
    --tlsv1.3 \
    --ech "ecl:AD7+DQA6WQAgACCVicJ2w8tUedISATcF6ThvruDbAfRKmuZTT+B5oyQGWgAEAAEAAQALZ2l0Lmt1cmEuZ2cAAA==" \
    https://git.kura.gg

... snip ...
* ECH: ECHConfig from command line
... snip ...
```


## openssl

```
$ dig +short HTTPS git.kura.gg
1 . alpn="h3" ipv4hint="46.62.173.123" ech="AD7+DQA6WQAgACCVicJ2w8tUedISATcF6ThvruDbAfRKmuZTT+B5oyQGWgAEAAEAAQALZ2l0Lmt1cmEuZ2cAAA==" ipv6hint="2a01:4f9:c013:f9a1::1"

$ docker run --rm --entrypoint openssl git.kura.gg/kura/forgejo/curl \
    s_client \
    -connect git.kura.gg:443 \
    -ech_config_list "AD7+DQA6WQAgACCVicJ2w8tUedISATcF6ThvruDbAfRKmuZTT+B5oyQGWgAEAAEAAQALZ2l0Lmt1cmEuZ2cAAA==" \
    -tls1_3 \
    -strict

... snip ...
---
ECH: success: 1
ECH: inner: git.kura.gg
ECH: outer: git.kura.gg
---
```
