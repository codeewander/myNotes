```bash
docker version # 確認 docker client 可以和 server engine 溝通  
docker info # 檢視和 docker engine 有關的設定檔

# 列出目前在執行中的 container  
docker container ls  
# 列出所有 container  
docker container ls -a  
# 列出 image  
docker image ls

# 先把 image 從 DockerHub 或其他 registry 上 pull 下來  
docker pull alpine:latest

docker run -it [image-id] # 根據 image 建立並執行 container

docker run -p 8080:8080 <image-id> # port mapping localhost port:container port

docker run -d redis # 讓該 container 在背景執行

# 希望能夠對某個執行中的 container 輸入一些指令  
docker exec -it <container-id> sh

docker start [container-id] # 執行已經建立過的某個 container  
docker stop [container-id] # 停止某個執行中的 container  
  
docker system prune # 把所有 docker 中當前沒用到的 container 清空  
  
# 將 container 包成 image 
#`-t` 是用來指定 Docker image 名稱, . 指的是當前位置
docker build -t kira/project_name .

```


#### docker image 
```bash
docker image ls     # 列出所有下載過的 image
```

#### docker run：根據 image 來建立並執行一個 container
```bash
# 根據 image 來建立並執行一個 container  
# docker run <image-name> <override-command>  
docker run hello-world  
docker run hello-world echo hello  
docker run hello-world ls  
  
# 執行 ubuntu 的 bash  
docker run -it ubuntu bash  
  
# port mapping (localhost:container) 
docker run -p 8080:8080 <image-id>
```

- `docker run` = `docker create` + `docker start`
- 執行 CLI 時會透過 docker client 告知 docker server (docker daemon) 要執行的任務，接著 docker server 會在本地的 _image cache_ 中找尋有無 `hello-world` 這個 image，找不到的話就會到 docker hub 上去找，找到後便把這個 image 拉到本機的 image cache 中，接著 docker server 會根據這個 image 建立 container 以執行程序。
- 原本的 image 中都會包含 Startup Command，若想針對這個 container 執行不同的 command，可以在 `docker run <image-id> [override command]` 後，使用 `override command`

#### docker create & docker start[​](https://pjchender.dev/devops/docker-command-line/#docker-create--docker-start "docker create & docker start的直接連結")

```bash
# Create a Container
docker create <image-name>   # 會取得 container id
# Start a Container
# -a：attached to the contained 並將 output 顯示在終端機上
docker start -a <container-id>
```

- `docker create` 的動作是根據 image 來建立 container，包含把 FS Snapshot 和 Startup Command 複製到 container 中
- `docker start` 會去執行 container 中啟動的指令（startup command）

#### docker exec：在 container 中執行額外的 command

```bash
docker run redis # 啟動 redis-server，container-id (11937697771a)  
  
# docker exec -it <container-id> <command>  
# -i 讓 STDIN 保持開啟  
# -t 讓 Terminal 介面比較好看（formatted）  
# -it 等於 -i -t，意思就是讓開發者可以輸入內容到 container  
docker exec -it 11937697771a redis-cli  
  
# 執行 container 的 bash shell，就可以進入該 container 的 shell 使用指令  
# 如此就不用一直重複使用 exec 的 指令  
docker exec -it <container-id> bash  
> redis-cli # 使用 Ctrl + D 可以離開
```