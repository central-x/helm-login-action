# Helm Login Action (OCI-based)
## 概述
&emsp;&emsp;用于在 GitHub Action 运行环境中登录基于 OCI 的 Helm 注册中心。

## 使用方法

```yaml
name: ci

on:
  push:

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - name: Helm Setup
        uses: azure/setup-helm@v3
        with:
          version: 3.14.0
      - name: Login to DockerHub
        uses: central-x/helm-login-action@v1
        with:
          registry: registry-1.docker.io
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - name: Push Helm Chart
        uses: central-x/helm-push-action@v1
        with:
          repository: oci://registry-1.docker.io/<username>
          chart: ./<path-to-chart>
```

## 自定义
### 输入参数（inputs）
&emsp;&emsp;以下输入参数可以用于 `steps.with`:

| 参数名称       | 类型     | 默认值                    | 必选 | 描述     |
|:-----------|--------|:-----------------------|:---|:-------|
| `registry` | String | `registry-1.docker.io` | 是  | 注册中心地址 |
| `username` | String | 无                      | 是  | 用户名    |
| `password` | String | 无                      | 是  | 密码     |

