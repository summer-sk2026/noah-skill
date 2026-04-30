# 组合工作流

## 先验证 CLI 再确认目标命令

```bash
noah --version
noah inspect trade get-account-info
noah inspect trade get-positions
noah inspect trade get-stock-amount
```

如果 `noah --version` 无输出，则先执行本 skill frontmatter 中的 `agent.install` 步骤，安装完成后再继续。安装时先确保 devDependencies 也被安装，这样 `npm run build` 所需工具才可用。安装成功后，实际调用时始终使用全局 `noah ...` 命令。

---

## Inspect 后执行 trade 命令

```bash
noah inspect trade get-account-info
noah inspect trade get-positions
noah inspect trade get-stock-amount
noah trade get-account-info
noah trade get-positions
noah trade get-stock-amount
```

---

## 结果总结建议

- 返回实际执行的命令
- 返回关键参数或 body 字段
- 返回核心结果摘要
- 如失败，直接总结错误原因
