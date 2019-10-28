# Docker commands list

## CRUD

### Create
- `docker build`
- `docker run`

### Retrieve
- `docker ps`
- `docker images`

### Update

### Delete
- `docker rmi`
- `docker image prune`
- `docker system prune`

### ETC
- `docker exec`

# In `react-app`
- `docker build -f Dockerfile.dev -t csyouk/react-app:latest .`
  - `-f Dockerfile.dev` : Dockerfile 지정해서 빌드 원할시 사용.
  - `-t` : tagging &rightarrow; **Format** : `(username)/(container name):(version)`
  - `.` : 현재 폴더 지칭.

- `docker run --rm --name=react-app -p 3000:3000 -v /app/node_modules -v $(pwd):/app 249bd5823ce6`
  - All options mappings are in this format `(host):(container)`
  - `--rm` option : remove container if container stopped
  - `--name` option : naming container
  - `-p` option : port config
  - `-v` option : volume mapping
  - `-p 3000:3000` &rightarrow; (local host port):(container port)
  - `-v /app/node_modules` &rightarrow; placeholder for that is inside the container. 즉, exclusive의 개념, -v option을 주면, host에 로컬의 파일들을 참조하게 되는데, placeholder를 주면, 해당 파일은 host의 파일을 참조하는게 아니라, container안에 파일을 참조한다.
  - `-v $(pwd):/app` &rightarrow; mapping (host directory):(container `/app` folder)
    - In this case, container does not store `/app` folder, get from host's volume.
    - 즉, 호스트에 저장하고, 컨테이너는 저장하시 않는 형식.

- `docker exec -it react-app /bin/sh`
  - `-i` : interactive mode
  - `-t` : pseudo terminal mode
  - `react-app` 이란 container 에 `/bin/sh` 라는 명령을 내리는 docker command. 실제로 하면 container에 접속됨.


