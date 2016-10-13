# Docker

#### Stop and remove all containers even if they're not running
```bash
$ docker stop $(docker ps -a -q)
$ docker rm $(docker ps -a -q)
```
