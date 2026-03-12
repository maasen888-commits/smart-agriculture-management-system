# Contributing

感谢你关注这个项目。

本项目欢迎改进建议、问题反馈、文档修正和代码贡献。为了让协作更高效，请先阅读下面的约定。

## 贡献方式

你可以通过以下方式参与：

- 提交 Bug 报告
- 提交新功能建议
- 修正文档、脚本或示例配置
- 改进前后端功能、测试和可观测性

## 开始之前

请先确认以下几点：

1. 不要提交真实密钥、真实系统 ID、客户资料、白皮书、账号导出文件。
2. 不要提交本地运行产物，例如日志、数据库文件、缓存目录、上传文件。
3. 涉及敏感信息的修改，请优先使用示例文件或占位值。
4. 大改动请先提 Issue，再开始实现，避免重复投入。

相关说明可参考：

- [README.md](./README.md)
- [docs/zero-to-one-setup-guide.md](./docs/zero-to-one-setup-guide.md)
- [docs/private-materials.md](./docs/private-materials.md)

## 本地开发

建议使用项目内统一脚本：

```bash
bash scripts/ops.sh restart-dev
```

常用初始化命令：

```bash
cp .env.example .env
cp frontend/.env.local.example frontend/.env.local
cp backend/.env.example backend/.env

cd frontend
npm install
npm run prisma:migrate
npm run prisma:generate
npm run seed:auth
```

## 分支与提交建议

建议从 `main` 拉出新分支进行开发。

分支命名建议：

- `feat/...`
- `fix/...`
- `docs/...`
- `refactor/...`

提交信息建议简洁明确，例如：

- `feat: add scheduler job history panel`
- `fix: prevent duplicate ws reconnect`
- `docs: improve deployment guide`

## 提交前自检

至少执行与你改动相关的检查。

基础建议：

```bash
bash scripts/verify.sh privacy
```

如果你改了业务链路，建议再执行：

```bash
bash scripts/verify.sh
```

如果你改了前端：

```bash
cd frontend
npm run build
```

如果你改了后端核心逻辑，建议至少确认：

- `/health` 正常
- 相关接口可用
- Celery / 调度任务没有明显回退

## Pull Request 要求

请尽量保证一个 PR 只解决一类问题。

PR 描述建议包含：

1. 背景与目标
2. 主要改动
3. 验证方式
4. 风险与回滚点
5. 截图或接口示例（如适用）

如果你的改动涉及以下内容，请在 PR 中明确说明：

- 数据库结构
- 权限控制
- 调度任务
- AI 结果生成逻辑
- 生产部署行为
- 隐私与开源边界

## Issue 提交建议

提 Issue 时请尽量提供：

- 发生环境
- 复现步骤
- 实际结果
- 预期结果
- 截图、日志、报错栈

这样会大幅提高问题定位效率。

## 安全与隐私

如果你发现的是密钥泄露、权限绕过、真实客户资料暴露等问题，请不要公开贴出敏感内容。

处理原则：

- 不在公开 Issue 中粘贴真实密钥
- 不上传包含客户信息的文件
- 不提交本地私有参数目录
- 优先使用占位值与脱敏示例

## 文档与语言

当前仓库以中文文档为主，代码注释与提交描述可中英结合，但请保持清晰、可维护。

## 行为约定

我们鼓励：

- 尊重事实
- 直接沟通
- 给出可复现信息
- 提供可落地建议

我们不鼓励：

- 含糊的“不能用”
- 缺少上下文的大段截图
- 把本地敏感信息直接贴进公共讨论

感谢你的贡献。
