# Docker Commands

 `docker network ls`

```
docker network ls

NETWORK ID     NAME                                       DRIVER    SCOPE
0f2cf91be0ce   bridge                                     bridge    local
b5073ce3792d   host                                       host      local
```

`docker network inspect 0f2cf91be0ce`


####  Delete volumes of a docker compose file

first, stop containers then delete
`docker compose stop`
`docker compose rm -v`
