# drools-dockerfile

Drools 的 Dockerfile 配置信息，可直接下载编译，快速搭建 Workbench 与 kie-server，并支持中文规则

使用步骤:
1. clone 项目到本地

   ```shell
   git clone https://github.com/qchery/drools-dockerfile.git
   ```

2. 进入 drools-workbench-showcase 目录，构建 Workbench 

   ```shell
   docker build -t qchery/drools-workbench-showcase:7.5.0.Final .
   ```

3. 进入 kie-server-showcase 目录，构建 Kie-Server

   ```shell
   docker build -t qchery/kie-server-showcase:7.5.0.Final .
   ```

4. 部署 Workbench

   ```shell
   docker run -p 8080:8080 -p 8001:8001 -d --name drools-wb qchery/drools-workbench-showcase:7.5.0.Final
   ```

5. 部署 Kie-Server

   ```shell
   docker run -p 8180:8080 -d --name kie-server --link drools-wb:kie_wb qchery/kie-server-showcase:7.5.0.Final
   ```

6. 访问 Workbench

   浏览器地址栏输入：http://localhost:8080/drools-wb
