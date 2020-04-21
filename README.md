# go-web-docker

构建镜像(普通用户操作)
```
sudo docker build \
         --build-arg USER_ID=$(id -u) \
         --build-arg GROUP_ID=$(id -g) \
         -t demo-math-app .
```

如果第一次使用，会先下载基础镜像，时间可能会长一些。

查看生成的镜像：
```
docker images
```

```
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
demo-math-app       latest              4bf11a9bd1be        About a minute ago   848 MB
docker.io/golang    1.14                a1c86c07867e        4 days ago           809 MB

```

demo-math-app为生成的镜像

步骤3：

```
sudo docker run -it --rm -p 8080:8080 -v $PWD/src:/go/src/demo-math-app  demo-math-app
```

验证结果，在浏览器地址中输入 `http://localhost:8080/sum/4/5

应该能看到以下内容：
```
The sum of 5 and 6 is 11
```

### 在生产环境使用Docker

构建发布的镜像：
```
$ sudo docker build -t demo-math-app-deploy -f Dockerfile.deploy .
```

发布测试：
```
$ sudo docker run -it -p 8010:8010 demo-math-app-deploy
```
