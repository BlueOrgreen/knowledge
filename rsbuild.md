📘 一、项目技术目标
项目目标	说明
快速启动	开发环境极速热更新，秒级冷启动
现代构建	使用 Rspack 构建，支持 HMR / Tree-shaking / 自动代码分割
多环境配置	支持 dev/test/prod 多环境构建输出
模块化开发	支持模块联邦、微前端拆分
类型安全	TypeScript 全面覆盖，支持 ESLint + Prettier
UI 框架	Ant Design 5 + Tailwind（可选）
接口管理	支持 mock / openAPI 自动生成
跨端适配	可扩展支持移动管理后台、小程序后台

🏗️ 二、技术栈选择
类型	技术	说明
构建工具	Rsbuild + Rspack	高性能替代 Webpack，支持模块联邦
框架	React 18 + React Router	标准化开发
组件库	Ant Design 5	企业级 UI，支持 token 与设计体系
状态管理	Zustand / Redux Toolkit	简洁状态管理
请求工具	Axios + swr / React Query	请求缓存 + 错误处理
Mock工具	msw / mockjs / mock-server	本地开发接口模拟
接口类型生成	OpenAPI Generator / @openapi-typescript	自动生成接口类型代码
样式	Tailwind CSS（可选） / SCSS module	高效样式管理
工程规范	ESLint + Prettier + Commitlint	项目规范统一化
CI/CD	GitHub Actions / GitLab CI	自动化构建与部署

🧪 三、技术探索点（建议调研方向）
探索项	说明
Rsbuild 插件机制	自定义插件体系，如何扩展构建流程（如 env 注入、Mock 注入）
构建性能	和 Webpack/Vite 对比，冷启动/热更新/构建耗时差异
模块联邦	如何拆分大型模块，比如「系统设置模块」独立部署
SSR 支持	探索 Rsbuild 的服务端渲染能力（若有需求）
设计体系 token 化	与 AntD v5 的 token 体系协同，对接设计平台（如 Figma）
接口自动化	基于 openAPI 文档自动生成 TS 类型 + 请求函数
多语言支持	接入 i18n 实现多语言国际化支持（如管理后台中英文切换）

📂 四、目录结构建议（适配 Rsbuild + React）
bash
复制
编辑
├── public/
├── src/
│   ├── assets/
│   ├── components/
│   ├── pages/
│   ├── layout/
│   ├── services/          # 请求层
│   ├── store/             # 状态管理
│   ├── router/            # 路由定义
│   ├── utils/
│   ├── constants/
│   └── App.tsx
├── rsbuild.config.ts      # Rsbuild 配置文件
├── .env                   # 环境变量
├── package.json
└── tsconfig.json
🛠️ 五、Rsbuild 初始配置关键点
ts
复制
编辑
// rsbuild.config.ts
import { defineConfig } from '@rsbuild/core';

export default defineConfig({
  source: {
    entry: './src/index.tsx',
  },
  html: {
    title: '中台管理系统',
  },
  output: {
    distPath: { root: 'dist' },
    filename: '[name].[contenthash:8].js',
  },
  tools: {
    // 可配置 babel、postcss、eslint、stylelint 等
  },
});
🔌 六、可选增强插件（建议后期探索）
@rsbuild/plugin-react: 支持 React 快速集成

@rsbuild/plugin-swc: 使用 swc 加速构建

@rsbuild/plugin-eslint: 持续集成代码规范

@rsbuild/plugin-openapi: 自动接口生成

@rsbuild/plugin-mock: 本地 mock 支持

🧭 七、后续建议探索路线
✅ 初步完成 Rsbuild + React 项目搭建

🧪 对比 Rsbuild 与 Webpack/Vite 性能差异

🧱 建立业务组件库（如表格、表单、权限按钮等）

🌐 接入 openAPI，接口定义自动化

🌈 自研一套轻量的主题切换系统（基于 token）

