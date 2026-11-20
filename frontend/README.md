# 前端说明

## 已实现功能

- Vue 3 + Vite 前端，使用 SVG 绘制地图和机器人。
- 从后端读取 16×12 地图、5 个障碍物和机器人状态。
- 支持前进、后退、左转、右转，通过后端接口执行。
- 显示位置、朝向、状态及越界、撞障碍提示。
- 请求期间禁用控制按钮，避免重复发送指令。
- 每 500ms 查询机器人状态，组件卸载时清理定时器。

## 本地启动

以下命令均从仓库根目录开始执行。

### 启动后端

首次使用时创建虚拟环境并安装依赖：

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

后续新开终端，在 backend 目录激活环境后启动：

```bash
source .venv/bin/activate
python -m uvicorn app.main:app --reload --port 8000
```

健康检查：http://127.0.0.1:8000/api/health

### 启动前端

另开终端，从仓库根目录执行：

```bash
cd frontend
npm ci
npm run dev
```

访问终端显示的 Local 地址，通常为 http://localhost:5173。
前端当前连接 http://127.0.0.1:8000，使用时需同时运行后端。

## 检查与验证

- 在 backend 目录激活虚拟环境，执行 `python -m pytest -q`：5 项通过。
- 在 frontend 目录执行 `npm run build`：通过。
- 手动验证：地图与障碍物显示、四个控制按钮、前后端坐标一致、
  越界拦截、障碍物拦截及受阻后恢复移动，均正常。
- 机器人状态保存在后端内存中，重启后端会恢复初始状态。

## 提交规则

不提交 .venv、node_modules 和 dist；保留 package-lock.json。
