## 1️⃣ 项目背景

在大型前端或微前端项目中，团队通常使用 `Monorepo` 架构管理多个子包。实际开发中遇到的问题包括：

多子包发布复杂、版本管理繁琐

手动生成 `CHANGELOG`、提交 `Git`、打 `tag` 易出错

多人协作时代码变更、依赖升级难以追踪

手动操作既容易出错，也降低效率，亟需自动化工具。

我设计并开发了 `dev-scripts` 工具，核心功能包括：

### 1. 版本管理与发布

- 支持 `Monorepo` 和 `Polyrepo` 模式
- 自动识别代码变更和依赖变动
- 生成 `CHANGELOG` 并同步更新版本号
- 自动提交 `version/CHANGELOG`、`打 tag`


### 2. CLI + 界面化交互

- 基于 `Commander.js` 封装命令
- 使用 `Inquirer` 提供交互式界面，降低操作出错率
- 发布流程中多次确认（Git 分支、工作区状态、tag、版本号）

### 3. Git 自动化管理

- 检查工作区是否干净
- 检查当前分支是否可发布
- 自动 commit、tag、push
- 支持 diff 提示，清晰展示变更内容和依赖树

### 4. 依赖管理

- Monorepo 下可自动更新子包依赖版本
- 检测依赖变动，支持可视化渲染依赖树
- 兼容 Monorepo 与 Polyrepo
- 对 monorepo 子包路径、tag 格式处理


### 5.可扩展性

- 功能模块化（update, diff, version, utils 等）
- 可轻松扩展新脚本和命令

## 3️⃣ 技术亮点

- Node.js 子进程管理：封装 execa 调用 Git 和 npm 命令，保证自动化执行
- 语义化版本控制：结合 semver 校验版本、生成 beta/alpha tag
- CHANGELOG 自动化生成：集成 conventional-changelog，自动维护日志
- Monorepo 感知：自动解析 packages/ 子包信息，支持依赖更新、代码变动检测
- 交互式 CLI：多轮交互（选择子包、确认版本、tag、发布方式），避免误操作
- 工程化实践：TypeScript + pnpm workspace + 模块化设计，保证可维护性和扩展性

## 4️⃣ 面试话术建议

面试腾讯时，你可以这样讲：

> 问题点：多子包发布流程复杂，手动操作容易出错。

解决方案：开发了 CLI 工具 dev-scripts，自动化完成发布流程，包括版本号管理、CHANGELOG 更新、Git commit/tag/push、依赖升级等。

技术实现：

- CLI 命令和交互式提示（Commander + Inquirer）
- Monorepo 子包信息解析与依赖变更检测
- 子进程管理（Execa） + npm/pnpm 发布自动化
- `Semver` 校验和 `tag` 格式约束
- 工程能力：模块化设计、可扩展、兼容 monorepo/polyrepo、多次确认机制降低出错概率。

> 价值：团队发布效率提升，减少人为失误，版本和日志管理自动化，支撑 CI/CD 流程。

## 5️⃣ 总结

核心价值：自动化、多包管理、版本可控、界面化交互

适用场景：腾讯类大型前端项目、微前端、多团队协作场景

---

# 项目自述（面试用）

> **项目名称**：`@fan-scripts/dev-scripts`  
> **项目类型**：Monorepo 辅助开发工具 / CLI  
> **技术栈**：Node.js, TypeScript, Commander.js, Inquirer, fs-extra, Execa  
> **目标公司**：腾讯  

### 项目背景

在大型 Monorepo 项目中，子包多、版本复杂、Git 分支操作频繁，开发和发布流程繁琐。手动操作容易出错，效率低下。

### 我的解决方案

- 封装 CLI 工具，提供统一入口 `dev-scripts`  
- 通过界面化交互减少手动输入错误  
- 集成 NPM 包发布、版本管理、CHANGELOG 自动生成  
- 自动处理 monorepo 多子包依赖  
- 封装工具函数，提供可复用的子包管理模块  

### 项目亮点（面试重点）

1. **自动化与效率**：大幅减少重复操作，支持界面化选择版本、子包、Git 分支  
2. **Monorepo 支持**：考虑多子包、多 workspace 的依赖管理和发布流程  
3. **可扩展性**：功能模块化，每个脚本独立，可快速扩展  
4. **技术深度**：涉及 Node.js 子进程管理、文件操作、命令行交互、版本语义化管理  
5. **工程实践**：结合 pnpm workspace、typescript、CLI 开发经验  

### 面试话术建议

- 强调 **解决了团队发布效率低、操作易错的问题**  
- 描述 **Monorepo 多子包管理的复杂性**，以及你的解决方案  
- 展示 **CLI + 界面化交互** 的设计思路和技术实现  
- 提及 **可扩展性和工程实践经验**，符合腾讯对工程能力的考察  

---

新增工具包

1. 开一个新分支,新增monorepo子包, 写完代码提交后执行发包命令, 会写入CHANGELOG文件