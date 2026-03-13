# MCP NPM Publish

将 Node.js/MCP 服务器项目转换为可发布到 npm 的包，并支持通过 `npx` 直接运行。

## 功能

- 配置 `package.json` 用于 npm 发布
- 添加 CLI bin 入口点，支持 `npx -y <package-name>` 执行
- 创建 `mcp.json` 用于 Claude Desktop 集成
- 验证包名是否可用

## 使用场景

当用户需要以下操作时使用此 skill：
- 将 Node.js 包发布到 npm registry
- 让包可通过 `npx -y <package-name>` 运行
- 配置 package.json 用于分发
- 为项目添加 CLI 命令入口
- 为 MCP 服务器创建 mcp.json 配置

## 快速开始

1. **配置 package.json** - 添加必要的字段（name, version, main, bin, files）
2. **添加 shebang** - 在 CLI 入口文件首行添加 `#!/usr/bin/env node`
3. **验证包名** - 检查 npm 上是否已有同名包
4. **创建 mcp.json** -（可选）用于 Claude Desktop 集成
5. **发布** - 运行 `npm publish --access public`

## 示例

配置后即可使用：

```bash
# 发布包
npm publish --access public

# 通过 npx 运行
npx -y your-package-name
```

## 详细文档

请参阅 [SKILL.md](./SKILL.md) 获取完整的工作流程和示例。
