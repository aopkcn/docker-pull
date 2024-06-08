#### 使用方法：自己动手，Fork 本项目，绑定你自己的仓库账号或其他镜像服务账号

1. 在 Fork 的项目中绑定账号
    - 如果要使用自建仓库镜像服务

      在 `Settings`-`Secrets and variables`-`Actions` 选择 `New repository secret` 新建 `DOCKER_USERNAME`（你的 Docker
      用户名） 和 `DOCKER_PASSWORD`（你的 Docker 密码） 两个 Secrets

    - 如果需要使用其它镜像服务，例如腾讯云、阿里云等

      在 `Settings`-`Secrets and variables`-`Actions` 选择 `New repository secret` 新建 `DOCKER_USERNAME`（你的其它镜像服务用户名）
      和 `DOCKER_PASSWORD`（你的其它镜像服务密码）两个 Secrets
      
2. 在 Fork 的项目中修改 `Settings`-`Actions`-`General` 中的 `Workflow permissions` 为 `Read and write permissions`

3. 在 `Actions` 里选择 `拉取镜像推送` ，在右边点击 `Run workfow`

4. 在输入框中填写：
    - 原镜像名称:版本 示例：`mysql/mysql-server`或者`ghcr.io/aopkcn/installers:debian`带域名
    - 同步后镜像名称:版本 示例`mysql-server:latest`或者`installers:debian`
    - 仓库地址 示例：`registry.cn-chengdu.aliyuncs.com`就是仓库域名地址
    - 空间名称 示例：`aopkcn`其中`ghcr.io/aopkcn/installers:debian`aopkcn就是空间名称
    - 系统架构 自行根据架构选择，如果拉取的镜像中没有将拉取失败，默认amd64

5. 最后点击 `Run workfow`等待镜像拉取推送

## 注意：自建仓库请保证GitHub能够访问，否则将无法推送！！！ 
