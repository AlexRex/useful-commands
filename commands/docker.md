# Docker

#### Remove all containers even if they're not running
`$ docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q) `
