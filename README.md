# MCU_VSCODE 下载与调试器

一款专为嵌入式开发者打造的 VS Code 插件，集成 OpenOCD 工具链，支持 ELF/SVD 文件快速查找、调试器与 MCU 核心配置，一键实现程序下载与调试，适配 ARM Cortex-M 等主流嵌入式架构。

## 核心功能

- 📁 自动搜索工作空间内的 ELF 可执行文件与 SVD 寄存器描述文件
- 🔧 内置 50+ 主流调试器配置（J-Link、ST-Link、CMSIS-DAP 等）
- 🖥️ 覆盖 200+ 常见 MCU 核心配置（STM32、ESP32、LPC、GD32 等系列）
- 🚀 一键启动 OpenOCD 调试（依赖 Cortex-Debug 插件）与程序下载
- 💻 自动适配 Windows 系统路径格式，解决跨平台路径兼容问题
- ⚙️ 支持自定义 OpenOCD 路径与默认 MCU 核心配置

## 前置依赖

1. 安装 [OpenOCD](https://openocd.org/) 工具链（建议添加到系统环境变量）
2. 安装 VS Code 插件 [Cortex-Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug)（调试功能依赖）
3. 确保工作空间已包含编译生成的 `.elf` 文件（程序镜像）

## 安装方法

### 方法 1：从 VS Code 插件市场安装
1. 打开 VS Code，进入「扩展」面板（Ctrl+Shift+X）
2. 搜索「MCU_VSCODE 下载与调试器」
3. 点击「安装」并重启 VS Code

### 方法 2：本地编译安装
1. 克隆本仓库到本地
2. 执行 `npm install` 安装依赖
3. 执行 `npm run compile` 编译 TypeScript 代码
4. 打开 VS Code，按 F5 启动插件开发环境（调试模式）

## 使用步骤

### 1. 打开工作空间
- 首先打开包含嵌入式项目的工作空间（必须包含 `.elf` 文件）
- 若未打开工作空间，插件会提示「请先打开一个工作空间！」

### 2. 启动插件
- 点击 VS Code 左侧活动栏的「MCU 调试工具」图标（图标为插件自定义图标）
- 插件会自动初始化，显示操作面板

### 3. 配置核心参数
1. **选择 ELF 文件**：点击「选择 ELF 文件」，从搜索结果中选择编译生成的 `.elf` 文件
2. **选择调试器**：点击「选择调试器」，选择与硬件匹配的调试器配置（如 ST-Link 选择 `stlink.cfg`）
3. **选择 MCU 核心**：点击「选择 MCU 核心」，选择目标 MCU 的核心配置（如 STM32F103 选择 `stm32f1x.cfg`）
4. **选择 SVD 文件（可选）**：点击「选择 SVD 文件」，选择对应 MCU 的 SVD 文件（用于调试时查看寄存器）

### 4. 执行核心操作
- **启动调试**：配置完成后，点击「启动调试」，插件会自动生成 Cortex-Debug 配置并启动调试会话
- **下载程序**：点击「下载程序」，插件会在专属终端中执行 OpenOCD 下载命令，完成后自动复位设备

### 5. 右键菜单快捷操作
- 在文件资源管理器中右键单击文件夹，可直接选择「MCU 调试」或「MCU 下载」，无需打开插件面板

## 配置说明

插件支持自定义配置，打开 VS Code 配置面板（Ctrl+,），搜索「MCU 调试工具配置」：

| 配置项 | 说明 | 默认值 |
|--------|------|--------|
| `mcu-vscode.openocdPath` | OpenOCD 可执行文件路径（若未设置则自动搜索系统环境变量） | 空字符串（自动搜索） |
| `mcu-vscode.defaultMcuCore` | 默认 MCU 核心类型（如 cortex-m0、cortex-m4 等） | `cortex-m4` |

## 常见问题

### Q1：未找到 ELF 文件？
- 检查工作空间中是否存在 `.elf` 文件（通常在 `build`、`bin` 目录下）
- 确保未过滤目标目录（插件默认排除 `node_modules` 目录）
- 重新编译项目生成最新的 `.elf` 文件

### Q2：调试启动失败？
- 检查 OpenOCD 是否已安装并配置环境变量（或在插件配置中指定 `openocdPath`）
- 确认调试器与 MCU 核心配置匹配（如 ST-Link 需选择 `stlink.cfg`，STM32F4 需选择 `stm32f4x.cfg`）
- 检查硬件连接（调试器与开发板是否正确接线，电源是否正常）

### Q3：Windows 系统路径错误？
- 插件已内置路径清洗功能，自动处理 Windows 路径格式（如将 `C:\project\app.elf` 转换为 `C:/project/app.elf`）
- 若仍有问题，可手动在插件配置中指定 OpenOCD 路径

### Q4：下载命令执行失败？
- 查看「OpenOCD 终端」中的错误信息（终端可通过「查看 > 终端」打开）
- 确认调试器与开发板连接正常，无硬件故障

## 技术支持

若遇到问题或有功能建议，可通过以下方式反馈：
- GitHub Issues：提交问题到本仓库的 Issues 板块
- 邮件反馈：发送问题描述到开发者邮箱（可在插件 package.json 中查看）

## 许可证

本插件基于 MIT 许可证开源，详见 [LICENSE](LICENSE) 文件。
