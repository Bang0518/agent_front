# 文化元宇宙Agent伴游系统

## 项目介绍

文化元宇宙Agent伴游系统是一个基于Vue 3和Vite构建的现代化Web应用，旨在提供沉浸式的文化体验和智能交互服务。该系统集成了先进的AI技术，为用户提供个性化的文化导览和交互体验。

## 技术栈

- Vue 3 - 渐进式JavaScript框架
- Vite - 下一代前端构建工具
- Vue SFC (Single File Components) - 单文件组件
- PNPM - 快速、节省磁盘空间的包管理器

## 功能特点

- 智能Agent交互
- 沉浸式文化体验
- 实时响应的用户界面
- 现代化的组件架构

## 快速开始

### 环境要求

- Node.js 16.0 或更高版本
- PNPM 包管理器

### 安装步骤

1. 克隆项目到本地
```bash
git clone [项目地址]
cd agent_front
```

2. 安装依赖
```bash
pnpm install
```

3. 启动开发服务器
```bash
pnpm dev
```

4. 构建生产版本
```bash
pnpm build
```

## 项目结构

```
├── src/                  # 源代码目录
│   ├── assets/          # 静态资源
│   ├── components/      # 组件
│   ├── App.vue          # 根组件
│   ├── main.js          # 入口文件
│   └── style.css        # 全局样式
├── public/              # 公共资源
├── index.html           # HTML模板
└── vite.config.js       # Vite配置
```

## 开发指南

- 组件开发遵循Vue 3的组合式API规范
- 使用`<script setup>`语法糖简化组件代码
- 采用模块化的开发方式，保持代码的可维护性

## 浏览器支持

- Chrome >= 87
- Firefox >= 78
- Safari >= 14
- Edge >= 88

## 作者

- 吴建军
- 董浩文

## 许可证

MIT License

Copyright (c) 2024 吴建军, 董浩文

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
