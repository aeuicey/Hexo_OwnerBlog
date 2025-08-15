# Hexo_OwnerBlog

[![Blog CI/CD](https://github.com/aeuicey/Hexo_OwnerBlog/actions/workflows/main.yml/badge.svg)](https://github.com/aeuicey/Hexo_OwnerBlog/actions/workflows/main.yml)
[![GitHub license](https://img.shields.io/github/license/aeuicey/Hexo_OwnerBlog)](https://github.com/aeuicey/Hexo_OwnerBlog/blob/main/LICENSE)

基于 Hexo 的个人博客项目，采用 arknights 主题，集成自动化部署流程，支持丰富的博客功能。

## ✨ 项目特点

- **主题特色**：使用 arknights 主题，支持明暗模式切换，自定义背景图片
- **功能完备**：包含文章归档、分类标签、搜索功能、代码高亮等
- **评论系统**：支持 Valine、Gitalk、Waline 等多种评论插件（可配置）
- **数学公式**：集成 KaTeX 支持，可渲染复杂数学公式
- **自动化部署**：通过 GitHub Actions 实现代码推送后自动构建部署
- **性能优化**：包含缓存机制、静态资源优化等

## 🚀 快速开始

### 本地开发环境搭建

1. 克隆仓库
   ```bash
   git clone https://github.com/aeuicey/Hexo_OwnerBlog.git
   cd Hexo_OwnerBlog
   ```

2. 安装依赖
   ```bash
   npm install
   ```

3. 启动本地服务器
   ```bash
   npm run server
   # 或使用 hexo 命令
   hexo server
   ```

4. 访问 `http://localhost:4000` 查看博客

### 常用命令

```bash
# 创建新文章
hexo new "文章标题"

# 生成静态文件
hexo generate
# 或
npm run build

# 清理生成文件
npm run clean

# 部署到远程
npm run deploy
```

## ⚙️ 配置说明

主要配置文件：
- `_config.yml`：Hexo 核心配置，包含站点信息、URL、目录结构等
- `_config.arknights.yml`：主题配置，包含主题样式、菜单、社交链接等

可自定义的关键配置：
- 站点信息：标题、副标题、作者等
- 主题设置：颜色模式、背景图片、导航菜单
- 评论系统：选择并配置适合的评论插件
- 部署设置：修改 `deploy` 部分配置部署目标

## 📦 部署方式

项目采用 GitHub Actions 实现自动化部署：
1. 推送代码到 `main` 或 `master` 分支
2. 触发 CI/CD 流程，自动执行依赖安装、构建
3. 部署到指定的 Git 仓库

需提前配置的 Secrets：
- `GH_TOKEN`：GitHub 访问令牌
- `GH_REF`：部署目标仓库地址
- `GIT_NAME`：提交者名称
- `GIT_EMAIL`：提交者邮箱

## 🎨 主题定制

- 自定义背景图片：修改 `_config.arknights.yml` 中的 `background_image` 配置
- 调整颜色模式：设置 `color` 选项（dark/light/auto 等）
- 添加社交链接：在 `social` 部分配置相关链接和图标
- 启用评论功能：选择一种评论系统并填写对应配置信息

## 📄 许可证

本项目采用 MIT 许可证 - 详情参见 [LICENSE](LICENSE) 文件

## 🔗 相关链接

- [Hexo 官方文档](https://hexo.io/docs/)
- [arknights 主题](https://github.com/...)
- [博客预览](https://github.alicetec.cn)
