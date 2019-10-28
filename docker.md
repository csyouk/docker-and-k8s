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


- `docker run --rm -it csyouk/react-app:latest npm run test`
  - Run `npm run test` using docker.


## Implement multi-step builds
- See [this](./react-app/Dockerfile).

- Output is like this.
```
~/workspace/udemy/react-app:master ✓ ➭ docker build -t csyouk/react-app_in_nginx:latest .
Sending build context to Docker daemon  158.9MB
Step 1/8 : FROM node:alpine as builder
 ---> 0fcfd7e52b09
Step 2/8 : WORKDIR '/app'
 ---> Using cache
 ---> 83f84624b154
Step 3/8 : COPY package.json .
 ---> Using cache
 ---> 4114453336c8
Step 4/8 : RUN npm install
 ---> Using cache
 ---> 6d90b2ac0676
Step 5/8 : COPY . .
 ---> 6b4e38affaa6
Step 6/8 : RUN npm run build
 ---> Running in 49f2d4caefe9

> react-app@0.1.0 build /app
> react-scripts build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:

  40.1 KB  build/static/js/2.7fcba3f7.chunk.js
  774 B    build/static/js/runtime-main.d247ced4.js
  611 B    build/static/js/main.efcfa5e1.chunk.js
  417 B    build/static/css/main.b100e6da.chunk.css

The project was built assuming it is hosted at the server root.
You can control this with the homepage field in your package.json.
For example, add this to build it for GitHub Pages:

  "homepage" : "http://myname.github.io/myapp",

The build folder is ready to be deployed.
You may serve it with a static server:

  npm install -g serve
  serve -s build

Find out more about deployment here:

  https://bit.ly/CRA-deploy

Removing intermediate container 49f2d4caefe9
 ---> b3054d90fe7c
Step 7/8 : FROM nginx
latest: Pulling from library/nginx
8d691f585fa8: Pull complete
5b07f4e08ad0: Pull complete
abc291867bca: Pull complete
Digest: sha256:922c815aa4df050d4df476e92daed4231f466acc8ee90e0e774951b0fd7195a4
Status: Downloaded newer image for nginx:latest
 ---> 540a289bab6c
Step 8/8 : COPY --from=builder /app/build /usr/share/nginx/html
 ---> 53814aed5faa
Successfully built 53814aed5faa
Successfully tagged csyouk/react-app_in_nginx:latest
```