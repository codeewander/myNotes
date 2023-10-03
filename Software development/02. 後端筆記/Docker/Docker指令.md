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