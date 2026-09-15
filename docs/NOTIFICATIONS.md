# 报告更新通知

CommitBrief 0.3.0 可在手动更新报告或智能总结成功后发送更新通知。侧栏“推送设置”可分别启用 macOS 系统通知和 Webhook。

筛选项目、作者或周期，编辑草稿，以及应用启动时的自动整理都不会推送。系统通知首次启用时会请求 macOS 权限。

## Webhook

远程地址必须使用 HTTPS；`localhost`、`127.0.0.1` 和 `::1` 可使用 HTTP。应用拒绝重定向，请直接填写最终地址。Webhook 地址可能包含凭证，因此单独保存在本机钥匙串。

应用发送 `POST` JSON，接收端返回任意 `2xx` 状态即视为成功：

```json
{
  "event": "report.updated",
  "title": "工作周报",
  "period": "week",
  "dateRange": "2026.09.09 — 2026.09.15",
  "projects": 2,
  "modules": 4,
  "workItems": 8,
  "commits": 12,
  "updatedAt": "2026-09-15T10:00:00Z"
}
```

Webhook 不包含报告正文、提交文本、仓库路径或 API Key。飞书、钉钉等要求固定消息结构的机器人地址不能直接使用，需要通过自己的转换 Webhook 接收以上 JSON 后转发。
