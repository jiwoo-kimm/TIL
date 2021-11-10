# 리스팅

- `docker ps <-a>`
- `docker images`

# 컨테이너

- `docker run <options> <IMAGE_NAME:IMAGE_VERSION>`
  - `<options>`
    - `-i` : foreground 실행, `-d` : background 실행
    - `-p <MACHINE_PORT:CONTAINER_PORT>` : Port forwaring from `MACHINE_PORT` to `CONTAINER_PORT`
- `docker restart <PID>`
- `docker attach <PID>`
- `docker commit <PID> <REPOSITORY>:<TAG>`
- `docker diff <PID>`:  이미지와 컨테이너의 차이 감지
- `docker rm <PID>`: 컨테이너 삭제

# 이미지

- `docker build -t <IMAGE_NAME:IMAGE_VERSION> <Dockerfile Path>`
- `docker rmi <IMAGE_NAME:IMAGE_VERSION>`: 이미지 삭제
