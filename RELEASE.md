# Release 流程说明

## 自动化 Release 流程

本项目使用 GitHub Actions 自动构建和发布应用程序。

### 触发方式

1. **自动触发**：推送代码到 `main` 或 `master` 分支时自动触发
2. **手动触发**：在 GitHub Actions 页面手动运行 workflow

### Release 流程

1. **更新版本号**
   - 修改 `package.json` 中的 `version` 字段
   - 修改 `src-tauri/tauri.conf.json` 中的 `version` 字段
   - 确保两个文件中的版本号一致

2. **提交并推送**
   ```bash
   git add package.json src-tauri/tauri.conf.json
   git commit -m "chore(release): bump version to x.x.x"
   git push origin main
   ```

3. **自动构建和发布**
   - GitHub Actions 会自动：
     - 安装依赖
     - 构建 Tauri 应用
     - 创建 tag（格式：`vx.x.x`）
     - 创建 GitHub Release
     - 上传构建产物（.msi、.exe 等）

### Tag 命名规则

- 格式：`v{version}`
- 示例：`v2.1.0`
- tag 会根据 `tauri.conf.json` 中的版本号自动创建

### Release 说明

- Release 会自动发布（非草稿）
- Release 标题：`Trae Account Manager v{version}`
- 包含下载说明和更新内容提示

### 注意事项

- 确保版本号遵循语义化版本规范（Semantic Versioning）
- 每次发布前确保代码已经过测试
- 不要手动创建 tag，让 workflow 自动处理
- 如需修改 release 说明，可以在 GitHub Release 页面手动编辑

### 手动触发 Release

如果需要重新构建某个版本：

1. 进入 GitHub 仓库的 Actions 页面
2. 选择 "Build and Release" workflow
3. 点击 "Run workflow"
4. 选择分支并运行

### 版本号管理建议

- 主版本号（Major）：不兼容的 API 修改
- 次版本号（Minor）：向下兼容的功能性新增
- 修订号（Patch）：向下兼容的问题修正

示例：
- `2.1.0` → `2.1.1`（bug 修复）
- `2.1.0` → `2.2.0`（新功能）
- `2.1.0` → `3.0.0`（重大更新）
