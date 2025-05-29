# GitHub Actions 配置

本项目使用以下 GitHub Actions 工作流：

## 工作流说明

### 1. CI/CD Pipeline (`ci-cd.yml`)
- **触发条件**: 推送到 `main` 或 `develop` 分支，或对 `main` 分支的 PR
- **功能**:
  - 在多个 Node.js 版本 (18.x, 20.x) 上构建和测试
  - 类型检查和构建验证
  - 自动部署到 GitHub Pages (仅 main 分支)

### 2. 依赖项更新 (`update-deps.yml`)
- **触发条件**: 每周一自动执行或手动触发
- **功能**:
  - 自动更新所有依赖项到最新版本
  - 如有更新，自动创建 PR

### 3. 发布工作流 (`release.yml`)
- **触发条件**: 推送版本标签 (如 `v1.0.0`)
- **功能**:
  - 构建生产版本
  - 生成变更日志
  - 创建 GitHub Release
  - 上传构建产物

### 4. 安全扫描 (`security.yml`)
- **触发条件**: 推送到 main 分支、PR 或每天定时执行
- **功能**:
  - 运行 npm audit 检查依赖项漏洞
  - 使用 CodeQL 进行代码安全分析
  - 检查高危漏洞并在发现时阻止流程

## 使用指南

### 设置 GitHub Pages
1. 在 GitHub 仓库设置中启用 Pages
2. 选择 "GitHub Actions" 作为源

### 创建发布版本
```bash
git tag v1.0.0
git push origin v1.0.0
```

### 手动触发依赖项更新
在 GitHub 仓库的 Actions 页面中找到 "Update Dependencies" 工作流，点击 "Run workflow"

## 环境变量
工作流使用以下内置的 GitHub secrets：
- `GITHUB_TOKEN`: 自动提供，用于 GitHub API 访问

## 注意事项
- 确保仓库名称与 `vite.config.ts` 中的 `base` 路径匹配
- 如果需要部署到自定义域名，请在 `public` 目录添加 `CNAME` 文件
- 可以根据需要启用 ESLint 和测试步骤
