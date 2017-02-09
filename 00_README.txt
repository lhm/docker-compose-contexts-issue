$ pwd
/tmp/dc

$ tree
.
├── p1
│   ├── Dockerfile
│   └── docker-compose.yml
└── p2
    ├── Dockerfile
    └── docker-compose.yml

2 directories, 4 files

$ cat p1/docker-compose.yml 
version: '2'
services:
  p1:
    build:
      context: .
    command: echo 'hello from p1'

$ cat p2/docker-compose.yml 
version: '2'
services:
  p2:
    build:
      context: .
    command: echo 'hello from p2'

$ docker-compose -f p1/docker-compose.yml -f p2/docker-compose.yml config
networks: {}
services:
  p1:
    build:
      context: /private/tmp/dc/p1
    command: echo 'hello from p1'
  p2:
    build:
      context: /private/tmp/dc/p1
    command: echo 'hello from p2'
version: '2.0'
volumes: {}

$ docker-compose -v
docker-compose version 1.10.0, build 4bd6f1a