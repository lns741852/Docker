## DockerFile 用途

- 將自己開發的程式包裝成 image 檔。

## 創建 Dockerfile

1. 專案下創建 Dockerfle 檔，不需附檔名。

2. 撰寫 Dockerfile

   ```
   ENV APP_DIR=/app
   FROM openjdk:17-oracle
   COPY ["./target/backend-app.jar", "/app/"]
   EXPOSE 8080
   WORKDIR ${APP_DIR}
   CMD ["java", "-jar", "backend-app.jar", "--spring.profiles.active=dev"]
   VOLUME  ${APP_DIR}/log
   LABEL description="A demo Spring Boot application." \ maintainer="foobar@gmail.com"
   ```

3. 建立映像檔

   - docker image build -t {映像檔名稱} -f {Dockerfile 檔名} {Dockerfile 所在路徑}

4. 指令查詢

| Docker      | Do                             | Remark                        |
| ----------- | ------------------------------ | ----------------------------- |
| FROM        | 指定執行環境                   | docker 會自動將環境檔拉入容器 |
| COPY        | 將主機的檔案與資料夾複製進容器 |
| EXPOSE      | 定義 port                      |
| WORKDIR     | 切換路徑                       | 如 linux cd                   |
| CMD         | 執行 cmd                       | 只能執行一次                  |
| ENV         | 宣告變數                       |
| ARG         | build 時傳入參數               | --build-arg {名稱}={值}       |
| VOLUME      | 預設掛載路徑                   |                               |
| LABEL       | 描述                           | docker image inspect 查看     |
| HEALTHCHECK | 顯示容器健康狀況               |                               |
