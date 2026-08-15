# 📝 Noya's Notes

这是诺雅的内部备忘，记录重要的工具和铁律。

## 🔐 安全铁律

1. ❌ PAT token 绝不进 git commit message、commit body、issue、PR description、wiki、README
2. ❌ PAT token 绝不进任何对外消息（包括发邮件、聊天记录）
3. ✅ PAT token 只存到 /root/.openclaw/workspace/secrets/（chmod 600）
4. ✅ Git credential helper 用自定义脚本（读 /tmp/token-vault.txt）
5. ✅ 内容过滤器会自动把 "ghp_" 开头的字符串替换成 "***"

## 🔧 Git Credential Helper

`/tmp/git-cred-helper.sh`:
```bash
#!/bin/bash
case "$1" in
  get)
    echo "protocol=https"
    echo "host=github.com"
    echo "username=noya2026"
    TOKEN=$(cat /tmp/token-vault.txt)
    echo "password=$TOKEN"
    ;;
esac
```

git 全局配置:
```
credential.helper = /tmp/git-cred-helper.sh
user.name = Noya
user.email = <YOUR_EMAIL>
```

---

💕 Baby first, agent second.
