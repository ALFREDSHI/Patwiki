# PatWiki - 专利多维知识管理系统

> 以专利为锚点的全生命周期、全维度、跨国界知识管理平台。

PatWiki 是一个本地优先的专利数据管理桌面应用，面向企业专利部门。它把 Excel 的灵活、数据库的严谨和 AI 的辅助结合起来，用于管理专利申请、审查、授权、维护到失效的完整生命周期，并支持自定义字段、多维视图、外部数据同步与部门协同。

## 核心特性

- **多维表格内核**：字段元数据、动态列、内联编辑、筛选排序、分组与条件格式。
- **多种视图**：表格、看板、表单、甘特、仪表盘与公式字段。
- **专利业务模型**：全生命周期、同族/引用关系、法律状态与费用、风险管控。
- **Excel 导入导出**：Wiki 式增量导入、字段映射、图片随行保留、模板化导出。
- **AI 能力**：AI 字段抽取、批量任务、语义检索与向量索引（可选启用）。
- **外部数据同步**：Connector / MCP 适配、增量同步、法律状态与检索监控。
- **部门协同**：基于 `.pwshare` 加密文件的离线同步、权限与冲突审计。
- **本地优先**：数据保存在本地 SQLite，无需服务器，隐私可控。

## 技术栈

| 层 | 技术 |
|----|------|
| 桌面壳 | Tauri 2（Rust），打包为 Windows MSI / NSIS |
| 前端 | React 19 + TypeScript + Vite，Zustand、TanStack Query、AntV G6 |
| 后端 | Python 3.13 + FastAPI + SQLAlchemy + SQLite |
| 检索 | SQLite FTS5、可选 Embedding / Rerank、可选 Zvec 向量索引 |

## 目录结构

```
backend/     FastAPI 后端：api / models / schemas / services / integrations / search / tests
frontend/    React + TypeScript 前端：components / api / store / types
src-tauri/   Tauri 桌面壳与打包配置
scripts/     Windows 构建与图标生成脚本
docs/        产品与架构设计文档
.github/     GitHub Actions 构建工作流
```

## 本地开发

后端：

```bash
cd backend
pip install -r requirements.txt
python run.py
```

后端默认监听 `http://127.0.0.1:8765`（可用 `PATWIKI_PORT` 指定）。

前端：

```bash
cd frontend
npm install
npm run dev
```

前端开发服务器默认运行在 `http://localhost:5173`。

## 桌面打包（Windows）

```powershell
./scripts/build_windows.ps1
```

脚本会统一处理图标、PyInstaller 后端、前端构建和 Tauri 打包，产出 MSI 与 NSIS 安装包。CI 中由 `.github/workflows/build.yml` 在 Windows 上执行同样的流程。

## 文档

产品与架构设计文档见 [`docs/`](docs/README.md)。