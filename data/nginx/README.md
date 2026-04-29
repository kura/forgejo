# Running
```
$ docker run --rm -v ./nginx.conf:/etc/nginx/nginx.conf git.kura.gg/kura/forgejo/nginx
```


## Notes
Requires at least this minimal configuration before the Lua module is compiled in.
```
http {
    lua_package_path "/usr/lib/lua/?.lua;;";
}
```
