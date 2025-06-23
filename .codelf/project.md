## Docker 镜像拉取推送工具 (Docker Image Pull & Push Tool)

> 一个基于 GitHub Actions 的 Docker 镜像拉取和推送自动化工具，支持从任意镜像仓库拉取镜像并推送到目标仓库

> 项目目的：解决 Docker 镜像在不同仓库间同步的问题，特别是从国外镜像仓库同步到国内镜像仓库，提高镜像拉取速度和可用性

> 项目状态：活跃开发中，支持多架构镜像同步

> 项目团队：个人开源项目

> 技术栈：GitHub Actions、Docker、Shell 脚本、YAML 配置



## Dependencies (GitHub Actions 和 Docker 依赖)

* actions/checkout@v2: GitHub Actions 官方代码检出动作
* Docker Engine: 容器运行时环境，用于镜像拉取、标记和推送操作
* Ubuntu Latest Runner: GitHub Actions 运行环境


## Development Environment

> 开发和运行环境要求

**必需环境：**
- GitHub 账号和仓库
- Docker 仓库账号（如 Docker Hub、阿里云、腾讯云等）
- 网络连接（能够访问源镜像仓库和目标镜像仓库）

**配置要求：**
- 在 GitHub 仓库的 Settings -> Secrets and variables -> Actions 中配置：
  - DOCKER_USERNAME: Docker 仓库用户名
  - DOCKER_PASSWORD: Docker 仓库密码

**运行方式：**
- 手动触发：在 Actions 页面点击 "Run workflow"
- 自动触发：当 images.txt 文件发生变化时自动运行


## Structure (项目结构详细分析)

> 项目结构简洁明了，主要包含 GitHub Actions 工作流配置和镜像列表文件

```
root
- .github/                          # GitHub 特定配置目录
    - workflows/                     # GitHub Actions 工作流目录
        - docker-pull.yml           # 【核心文件】主要的镜像拉取推送工作流
                                     # 功能：定义完整的镜像同步流程
                                     # 支持多架构：amd64, arm64, arm/v7, arm/v6, 386, s390x, ppc64le
                                     # 工作流程：检出代码 -> 读取镜像列表 -> 登录仓库 -> 拉取标记推送镜像
                                     # 输入参数：镜像文件路径、目标仓库地址、空间名称、系统架构
                                     # 错误处理：包含登录失败和推送失败的检查机制
- .gitignore                        # Git 忽略文件配置
- README.md                         # 【重要文件】项目说明文档
                                     # 包含详细的使用方法和配置步骤
                                     # 说明如何 Fork 项目、配置密钥、运行工作流
                                     # 提供了完整的操作示例和注意事项
- images.txt                        # 【核心文件】镜像列表配置文件
                                     # 格式：每行一个镜像，格式为 image:tag
                                     # 当前包含：goharbor/harbor-portal:v2.12.1, goharbor/harbor-core:v2.12.1
                                     # 文件变更会自动触发工作流执行
```
