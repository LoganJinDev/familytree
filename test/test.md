🛠 环境准备
安装 Docker 和 Docker Compose

确保您的系统已安装 Docker 和 Docker Compose。

获取项目代码

克隆项目仓库：

bash
复制
编辑
git clone https://github.com/qiaoshouqing/familytree.git
cd familytree
🐳 创建 Dockerfile
在项目根目录下创建一个名为 Dockerfile 的文件，内容如下：​

Docker
复制
编辑
   # 使用官方 Node.js 镜像作为基础镜像
   FROM node:18-alpine

   # 设置工作目录
   WORKDIR /app

   # 复制 package.json 和 pnpm-lock.yaml
   COPY package.json pnpm-lock.yaml ./

   # 安装 pnpm
   RUN npm install -g pnpm

   # 安装项目依赖
   RUN pnpm install

   # 复制项目源代码
   COPY . .

   # 构建项目
   RUN pnpm build

   # 暴露应用运行的端口
   EXPOSE 3000

   # 启动应用
   CMD ["pnpm", "start"]
🧪 创建 Docker Compose 配置（可选）
为了方便管理容器，您可以创建一个 docker-compose.yml 文件：​

yaml
复制
编辑
   version: '3.8'
   services:
     familytree:
       build: .
       ports:
         - "3000:3000"
       environment:
         - NODE_ENV=production
       volumes:
         - .:/app
⚙️ 配置项目
设置环境变量

复制 .env.local.example 文件并重命名为 .env.local，根据需要修改其中的配置项。

准备家庭数据

将您的家庭数据转换为 JSON 格式，并保存到 config/family-data.json 文件中。

🚀 构建并启动容器
构建镜像

如果使用 Dockerfile：

bash
复制
编辑
docker build -t familytree .
启动容器

如果使用 Docker Compose：

bash
复制
编辑
docker-compose up
如果使用 Docker 命令：

bash
复制
编辑
docker run -p 3000:3000 familytree
🌐 访问应用
在浏览器中访问 http://localhost:3000，即可查看您的家庭树应用。​

