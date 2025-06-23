# Docker 镜像拉取推送工具

一个基于 GitHub Actions 的 Docker 镜像自动同步工具，支持从任意镜像仓库拉取镜像并推送到目标仓库。

## ✨ 主要特性

- 🚀 **自动触发**：修改 `images.txt` 文件自动触发镜像同步
- 🎯 **手动控制**：支持手动触发并自定义参数
- 🏗️ **多架构支持**：支持 amd64、arm64、arm/v7、arm/v6、386、s390x、ppc64le
- 📝 **智能解析**：自动解析镜像名称和标签，支持注释和空行
- 📊 **详细日志**：提供清晰的执行状态和结果统计
- 🛡️ **错误处理**：完善的错误检查和状态反馈机制

## 🚀 快速开始

### 1. Fork 项目并配置密钥

1. Fork 本项目到你的 GitHub 账号
2. 在你的项目中配置仓库密钥：
   - 进入 `Settings` → `Secrets and variables` → `Actions`
   - 点击 `New repository secret` 添加以下密钥：
     - `DOCKER_USERNAME`：你的 Docker 仓库用户名
     - `DOCKER_PASSWORD`：你的 Docker 仓库密码

### 2. 配置镜像列表

编辑 `images.txt` 文件，添加需要同步的镜像：

```
# 格式：镜像名称:标签
nginx:latest
redis:7-alpine
goharbor/harbor-core:v2.12.1
registry.k8s.io/pause:3.9
```

### 3. 触发同步

#### 方式一：自动触发（推荐）
- 直接修改并提交 `images.txt` 文件
- GitHub Actions 会自动检测文件变更并触发同步
- 使用默认配置：阿里云仓库 + amd64 架构

#### 方式二：手动触发
1. 进入 `Actions` 页面
2. 选择 `拉取镜像推送` 工作流
3. 点击 `Run workflow`
4. 填写自定义参数：
   - **镜像列表文件路径**：默认 `images.txt`
   - **仓库地址**：如 `registry.cn-chengdu.aliyuncs.com`
   - **空间名称**：如 `your-namespace`
   - **系统架构**：选择目标架构

## 📋 配置说明

### 默认配置（自动触发时使用）
- **目标仓库**：`crpi-4a2bcohw4rh1g57m.cn-guangzhou.personal.cr.aliyuncs.com`
- **空间名称**：`xin-devops`
- **系统架构**：`amd64`
- **镜像文件**：`images.txt`

### 镜像文件格式
- 每行一个镜像，格式：`镜像名称:标签`
- 支持完整域名：`registry.k8s.io/kube-apiserver:v1.28.0`
- 支持简单名称：`nginx:latest`
- 以 `#` 开头的行为注释
- 空行会被自动忽略

## 📊 执行结果

工作流会提供详细的执行信息：
- ✅ 成功同步的镜像数量
- ❌ 失败的镜像及原因
- 📈 完整的处理统计
- 🔍 每个镜像的详细处理日志

## ⚠️ 注意事项

- 确保 GitHub 能够访问你的目标仓库
- 检查仓库凭据的正确性
- 某些镜像可能不支持指定的架构
- 网络连接稳定性会影响同步成功率
- 大量镜像同步可能需要较长时间
