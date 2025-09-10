# 逸小仙桌宠系统

> 基于Tauri框架开发的智能桌面宠物应用，结合A2A模式后端架构的校园助手系统

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Tauri](https://img.shields.io/badge/Tauri-2.8.0-purple.svg)](https://tauri.app/)
[![React](https://img.shields.io/badge/React-18.3.1-blue.svg)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)

## ✨ 项目特色

### 🎮 桌面宠物功能
- **全屏透明窗口**：覆盖整个桌面，背景完全透明
- **始终置顶显示**：桌宠始终显示在其他应用之上
- **点击穿透技术**：不影响正常桌面操作
- **双模式显示**：经典原像 + Q萌心情动画
- **智能交互**：拖拽移动、右键菜单、AI对话

### 🤖 智能校园助手
- **A2A架构**：Agent-to-Agent智能处理模式
- **智能对话**：基于腾讯云Agent的AI对话系统
- **校园服务**：简单问题自动化，复杂问题人工介入
- **多角色支持**：辅导员、招生、微信等不同对话风格

## 🚀 快速开始

### 环境要求
- **Node.js**: 18.0+
- **Rust**: 1.77+
- **操作系统**: macOS 10.15+ / Windows 10+ / Linux

### 安装步骤

1. **克隆项目**
```bash
git clone https://github.com/wuyuyang001-oss/-.git
cd SYS_DesktopPet_4
```

2. **安装依赖**
```bash
npm install
```

3. **启动开发模式**
```bash
# 加载Rust环境（macOS/Linux）
source ~/.cargo/env

# 启动桌宠
npm run tauri:dev
```

4. **构建应用**
```bash
npm run tauri:build
```

## 🎨 功能展示

### 桌宠状态
- **经典原像**：传统桌宠形象，支持旋转动画
- **Q萌心情**：6种表情动画
  - 🎶 哼个小曲
  - ❤️ 发射心心
  - 😀 畅快大笑
  - 🤔 我在思考
  - 🦆 顶住鸭力
  - 👍 赞赞能量

### 交互功能
- **点击桌宠**：打开AI对话窗口
- **拖拽移动**：自由调整桌宠位置
- **右键菜单**：切换状态、设置、通知等
- **智能对话**：多角色AI助手

## 🛠️ 技术架构

### 前端技术栈
- **框架**: React 18.3.1 + TypeScript
- **构建工具**: Vite 6.3.5
- **桌面框架**: Tauri 2.8.0
- **UI组件**: Radix UI + Tailwind CSS
- **动画**: Motion (Framer Motion)
- **状态管理**: React Hooks + LocalStorage

### 后端架构
- **桌面后端**: Rust + Tauri
- **AI服务**: 腾讯云Agent集成
- **A2A模式**: Agent-to-Agent智能处理

### 项目结构
```
src/
├── components/          # React组件
│   ├── DesktopPet.tsx  # 桌宠主体组件
│   ├── ChatDialog.tsx  # AI对话组件
│   ├── SettingsPanel.tsx # 设置面板
│   └── ui/             # UI组件库
├── hooks/              # 自定义Hooks
│   ├── useClickThrough.ts # 点击穿透
│   ├── usePetSettings.ts  # 桌宠设置
│   └── useNotifications.ts # 通知管理
├── services/           # 服务层
│   └── aiService.ts    # AI服务接口
├── data/               # 数据配置
│   └── characters.ts   # 角色配置
└── types/              # 类型定义

src-tauri/              # Tauri后端
├── src/
│   └── lib.rs         # Rust主代码
└── Cargo.toml         # Rust依赖
```

## 🎯 核心功能实现

### 点击穿透技术
```typescript
// 前端检测鼠标位置
const handleMouseMove = (e: MouseEvent) => {
  const isOverPet = checkMouseOverPet(e.clientX, e.clientY);
  setClickThrough(!isOverPet);
};

// Rust后端设置窗口属性
#[tauri::command]
fn set_click_through(window: Window, enabled: bool) -> Result<(), String> {
    window.set_ignore_cursor_events(enabled).map_err(|e| e.to_string())
}
```

### 动画系统
```typescript
// 帧动画实现
const EmojiAnimation = ({ mood, frame }: { mood: string; frame: number }) => {
  return (
    <motion.img
      src={`/emoji/${mood}_${frame.toString().padStart(2, '0')}.png`}
      animate={{ opacity: [0, 1, 0] }}
      transition={{ duration: 0.2, repeat: Infinity }}
    />
  );
};
```

## 📱 使用说明

### 基本操作
1. **启动桌宠**：运行 `npm run tauri:dev`
2. **移动桌宠**：直接拖拽到任意位置
3. **打开对话**：点击桌宠打开AI对话
4. **切换状态**：右键选择不同心情
5. **调整设置**：右键 → 设置

### 高级功能
- **透明度调节**：在设置中调整桌宠透明度
- **大小调整**：支持小、中、大三种尺寸
- **通知管理**：查看系统通知和提醒
- **角色切换**：选择不同的AI助手角色

## 🔧 开发指南

### 添加新心情
1. 在 `src/data/characters.ts` 中添加新心情配置
2. 准备8帧PNG图像，命名格式：`{moodId}_01.png` 到 `{moodId}_08.png`
3. 将图像放置在 `public/emoji/` 目录

### 自定义角色
1. 在 `src/data/characters.ts` 中定义新角色
2. 添加角色图像到 `public/characters/` 目录
3. 配置角色的对话风格和功能

## 🐛 故障排除

### 常见问题
1. **桌宠不显示**：检查终端错误信息，确保端口3000未被占用
2. **点击穿透失效**：
   - macOS：系统偏好设置 → 安全性与隐私 → 隐私 → 辅助功能
   - Windows：以管理员权限运行
3. **动画卡顿**：检查系统性能，关闭其他占用资源的应用

### 调试技巧
- 使用浏览器开发者工具调试前端
- 查看Tauri控制台输出
- 检查系统日志中的错误信息

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开 Pull Request

## 📞 联系方式

- 项目链接：[https://github.com/wuyuyang001-oss/-](https://github.com/wuyuyang001-oss/-)
- 问题反馈：[Issues](https://github.com/wuyuyang001-oss/-/issues)

## 🙏 致谢

感谢以下开源项目的支持：
- [Tauri](https://tauri.app/) - 跨平台桌面应用框架
- [React](https://reactjs.org/) - 用户界面库
- [Radix UI](https://www.radix-ui.com/) - 无障碍UI组件
- [Framer Motion](https://www.framer.com/motion/) - 动画库

