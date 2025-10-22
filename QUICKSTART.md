# Git 平台 OAuth 配置指南

本文档介绍如何为 Woodpecker CI 配置 GitHub、GitLab 和 Gitea 的 OAuth 应用。

**官方文档链接：**
- [Server Configuration](https://woodpecker-ci.org/docs/administration/configuration/server)
- [GitHub Configuration](https://woodpecker-ci.org/docs/administration/configuration/forges/github)
- [GitLab Configuration](https://woodpecker-ci.org/docs/administration/configuration/forges/gitlab)
- [Gitea Configuration](https://woodpecker-ci.org/docs/administration/configuration/forges/gitea)

## GitHub OAuth 应用创建

**重要提示：** 使用 GitHub 时，需要将 `WOODPECKER_GITHUB=true`，并确保其他 Git 平台的开关（如 `WOODPECKER_GITLAB` 和 `WOODPECKER_GITEA`）设置为 `false`。

以下步骤介绍如何在 GitHub 上为 Woodpecker 创建 OAuth 应用，并获取 `Client ID` 与 `Client Secret`：

1. 登录 GitHub，点击右上角头像，依次进入 `Settings` → `Developer settings` → `OAuth Apps`，点击 `New OAuth App`。
2. 在表单中填写以下信息：
   - `Application name`：自定义名称，例如 `Woodpecker CI`。
   - `Homepage URL`：Woodpecker 对外访问地址，例如 `https://ci.example.com`。
   - `Authorization callback URL`：Woodpecker 回调地址，格式为 `<WOODPECKER_HOST>/authorize`，例如 `https://ci.example.com/authorize`。
3. 点击 `Register application` 完成创建后，页面会出现 `Client ID`。记下该值并填入 Woodpecker 的 `WOODPECKER_GITHUB_CLIENT`。
4. 在应用详情页点击 `Generate a new client secret`，复制生成的密钥并填入 `WOODPECKER_GITHUB_SECRET`。注意生成的密钥只显示一次，如遗失需要重新生成。
5. 确认 Woodpecker 的环境变量包含 `WOODPECKER_GITHUB_SCOPE=user:email,read:org`，以确保授权流程能够获取用户邮箱和组织信息。

完成以上步骤后，将部署配置中的相关变量更新为对应的 `Client ID` 与 `Client Secret`，即可在 Woodpecker 中使用 GitHub 登录。

---

## GitLab OAuth 应用创建

**重要提示：** 使用 GitLab 时，需要将 `WOODPECKER_GITLAB=true`，并确保其他 Git 平台的开关（如 `WOODPECKER_GITHUB` 和 `WOODPECKER_GITEA`）设置为 `false`。

以下步骤介绍如何在 GitLab 上为 Woodpecker 创建 OAuth 应用：

1. 登录 GitLab，点击右上角头像，依次进入 `Edit profile` → `Applications`。
2. 在 `Add new application` 表单中填写以下信息：
   - `Name`：自定义名称，例如 `Woodpecker CI`。
   - `Redirect URI`：Woodpecker 回调地址，格式为 `<WOODPECKER_HOST>/authorize`，例如 `https://ci.example.com/authorize`。
   - `Scopes`：勾选以下权限：
     - `api` - 访问 API
     - `read_user` - 读取用户信息
     - `read_repository` - 读取仓库
3. 点击 `Save application` 完成创建后，页面会显示 `Application ID` 和 `Secret`。
4. 配置 Woodpecker 环境变量：
   - `WOODPECKER_GITLAB=true`
   - `WOODPECKER_GITLAB_URL=https://gitlab.com`（如果是自建 GitLab，填写对应的 URL）
   - `WOODPECKER_GITLAB_CLIENT=<Application ID>`
   - `WOODPECKER_GITLAB_SECRET=<Secret>`

**注意**：如果使用自建 GitLab 实例，需要将 `WOODPECKER_GITLAB_URL` 设置为实际的 GitLab 地址。

---

## Gitea OAuth 应用创建

**重要提示：** 使用 Gitea 时，需要将 `WOODPECKER_GITEA=true`，并确保其他 Git 平台的开关（如 `WOODPECKER_GITHUB` 和 `WOODPECKER_GITLAB`）设置为 `false`。

以下步骤介绍如何在 Gitea 上为 Woodpecker 创建 OAuth 应用：

1. 登录 Gitea，点击右上角头像，依次进入 `Settings` → `Applications`。
2. 在 `Manage OAuth2 Applications` 区域，点击 `Create a new OAuth2 Application`。
3. 在表单中填写以下信息：
   - `Application Name`：自定义名称，例如 `Woodpecker CI`。
   - `Redirect URI`：Woodpecker 回调地址，格式为 `<WOODPECKER_HOST>/authorize`，例如 `https://ci.example.com/authorize`。
4. 点击 `Create Application` 完成创建后，页面会显示 `Client ID` 和 `Client Secret`。
5. 配置 Woodpecker 环境变量：
   - `WOODPECKER_GITEA=true`
   - `WOODPECKER_GITEA_URL=https://gitea.example.com`（填写 Gitea 实例的 URL）
   - `WOODPECKER_GITEA_CLIENT=<Client ID>`
   - `WOODPECKER_GITEA_SECRET=<Client Secret>`

**注意**：Gitea 通常为自建服务，请确保 `WOODPECKER_GITEA_URL` 设置为正确的 Gitea 实例地址。

---

# Woodpecker CI 配置示例

以下是一个简单的 Woodpecker CI 配置文件示例,可以直接在项目根目录创建 `.woodpecker.yml` 文件使用:

```yaml
kind: pipeline
type: docker
name: default

steps:
  - name: greet
    image: alpine:latest
    commands:
      - echo "hello woodpecker"
```

该配置文件会在每次代码推送时运行一个简单的任务,使用 Alpine Linux 镜像输出 "hello woodpecker" 消息。你可以基于此示例扩展更多构建、测试和部署步骤。
