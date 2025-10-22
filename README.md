# Woodpecker CI for Lazycat 平台

将强大的开源持续集成系统 Woodpecker CI 移植到 Lazycat 平台,让您可以轻松部署和使用这个简单而强大的 CI/CD 工具。

## 项目简介

Woodpecker CI 是一个简单而强大的持续集成系统,专注于 Docker 容器化工作流。本项目将 Woodpecker CI 适配到 Lazycat 平台,使您能够在 Lazycat 上快速部署和管理自己的 CI/CD 环境。

## 主要功能

- **容器化构建**: 基于 Docker 的构建环境,每次构建都在隔离的容器中运行
- **多平台支持**: 支持 GitHub、GitLab、Gitea 等多种代码托管平台
- **灵活的流水线配置**: 使用简单的 YAML 配置文件定义构建流水线
- **插件生态系统**: 丰富的插件支持,可扩展各种构建和部署需求
- **多 Agent 架构**: 支持多个构建 Agent,可横向扩展构建能力
- **实时日志**: 实时查看构建日志和构建状态

## 快速开始

在 Lazycat 平台上,您可以一键部署 Woodpecker CI,无需手动配置 Docker 环境。

### 部署步骤

1. 登录 [Lazycat 平台](https://lazycat.cloud)
2. 在应用市场中找到 Woodpecker CI
3. 点击"一键部署"
4. 按照向导配置必要的参数:
   - GitHub/GitLab OAuth 凭证
   - 服务访问域名
   - 其他可选配置
5. 等待部署完成,即可开始使用

### 配置说明

部署时需要配置以下关键参数:

- **代码托管平台集成**: 配置 GitHub、GitLab 或 Gitea 的 OAuth 应用
- **访问域名**: 设置 Woodpecker 服务的外部访问地址
- **Agent 密钥**: 用于 Server 和 Agent 之间的安全通信

## 致谢

感谢 Woodpecker CI 团队和开源社区为我们提供了这个优秀的持续集成工具。本项目基于官方 Woodpecker CI 文档 (https://woodpecker-ci.org/docs/3.10/administration/installation/docker-compose) 进行移植和适配。

## 版权说明

- 本配置文件和移植工作: Apache License 2.0 © 2025 Lazycat Apps
- Woodpecker CI 软件本身: Apache License 2.0 © 2018 Drone.IO Inc., 2020 Woodpecker Authors

详见项目根目录下的 [LICENSE](LICENSE) 文件。

## 相关链接

- **Woodpecker CI 官网**: https://woodpecker-ci.org
- **Woodpecker CI 源代码**: https://github.com/woodpecker-ci/woodpecker
- **Woodpecker CI 文档**: https://woodpecker-ci.org/docs
- **Lazycat 平台**: https://lazycat.cloud
