---
name: mcp-npm-publish
description: Transform MCP server Node.js projects into npm-publishable packages with npx executable support. Use when user wants to publish MCP server to npm registry, make it executable via npx -y, configure package.json for distribution, or add CLI bin entry points.
---

# MCP NPM Publish Skill

Transform Node.js/MCP server projects into npm-publishable packages with npx executable support.

## When to Use This Skill

Use this skill when you need to:
- Publish a Node.js package to npm registry
- Make a package executable via `npx -y <package-name>`
- Configure package.json for npm distribution
- Add CLI bin entry points to a project
- Create mcp.json for MCP server integration

## Workflow

### Step 1: Read package.json

Check current configuration and identify missing fields.

### Step 2: Update package.json

**Required for npm publish:**
```json
{
  "name": "unique-package-name",
  "version": "1.0.0",
  "main": "dist/index.js"
}
```

**Required for npx execution:**
```json
{
  "bin": {"command-name": "./dist/cli.js"},
  "files": ["dist"]
}
```

**Recommended(Answer the user):**
- `description`, `author`, `license`, `repository`, `keywords`

### Step 3: Add shebang to CLI entry

Add to first line of bin entry file:
```javascript
#!/usr/bin/env node
```


### Step 4: Verify Package and project structure
1. Recheck that the content has been completed.
2. Verify that the package name is unique and not already taken on npm registry:
```bash
npm view package-name.
```
If the package name is duplicated, provide naming suggestions based on the user's current package name and recheck if it exists.


### Step 5: Create mcp.json (for MCP servers)

Create `.mcp.json` in project root for Claude Desktop integration:

```json
{
  "mcpServers": {
    "your-server-name": {
      "command": "npx",
      "args": ["-y", "your-package-name"]
    }
  }
}
```

**Example:**
```json
{
  "mcpServers": {
    "my-mcp-server": {
      "command": "npx",
      "args": ["-y", "@username/my-mcp-server"]
    }
  }
}
```

**For local development:**
```json
{
  "mcpServers": {
    "my-mcp-server": {
      "command": "node",
      "args": ["/absolute/path/to/your-project/dist/index.js"]
    }
  }
}
```

### Step 6: Publish (Guide user)

Ask the user: "Does it need to be published to the npm repository?"

If user confirms yes, guide them through the process:

**Prerequisites (user must complete first):**
1. Register at https://www.npmjs.com/signup
2. Verify email address
3. Enable 2FA (required for publishing)

**Publish steps:**
```bash
# Login (will open browser for auth if 2FA enabled)
npm login

# Publish
npm publish --access public
```

**Test after publish:**
```bash
npx -y your-package-name
```

If user says no, skip this step. The project is already configured and ready to publish later.

## Examples

**Example 1: Add npx support**
```json
// package.json
{
  "name": "my-cli",
  "bin": {"my-cli": "./dist/cli.js"},
  "files": ["dist"]
}
```

```javascript
// dist/cli.js - first line
#!/usr/bin/env node
```

**Example 2: Scoped package**
```json
{
  "name": "@username/package-name",
  "version": "1.0.0",
  "main": "dist/index.js",
  "bin": {"my-command": "./dist/cli.js"},
  "files": ["dist"],
  "license": "MIT"
}
```
