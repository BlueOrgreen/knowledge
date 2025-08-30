
# Monorepo感知

在 `Monorepo` 下，子包都在 `packages/` 目录下

```tsx
packages/
  dev-scripts/
    package.json
  utils/
    package.json
  web-app/
    package.json

```

目标是：

1. 自动扫描所有子包信息
2. 检测哪些包有代码变动或依赖变动
3. 支持依赖更新或发包时，精准定位子包


## 核心实现函数


### 获取子包信息

```tsx
export const getMonorepoPkgListInfo = async (): Promise<Pkg[]> => {
  const pkgInfoList: Pkg[] = []
  const targetDirPath = path.resolve(process.cwd(), './packages')
  const pkgDirList = await fs.readdir(targetDirPath)

  for (const pkgDir of pkgDirList) {
    const pkgDirPath = path.join(targetDirPath, pkgDir)
    const pkgJsonFilePath = path.join(pkgDirPath, 'package.json')
    if (await fs.pathExists(pkgJsonFilePath)) {
      const { name: pkgName, version: pkgCurrentVersion } =
        await fs.readJSON(pkgJsonFilePath)
      pkgInfoList.push({
        pkgDir,
        pkgDirPath,
        pkgJsonFilePath,
        pkgName,
        pkgCurrentVersion,
      })
    }
  }

  return pkgInfoList
}
```

分析：

1. 扫描 `packages/` 目录
2. 对每个子目录，检查是否有 `package.json`
3. 提取：
    - `pkgName`：包名
    - `pkgCurrentVersion`：当前版本
    - `pkgDirPath`、`pkgJsonFilePath`：路径信息
4. 返回一个数组，方便后续操作

### 检测代码变动

```tsx
const diffPkgList = await addDiffInfoForPkgListInMonorepo(pkgList)
```

- `addDiffInfoForPkgListInMonorepo` 遍历每个包
- 使用 `git log <latestTag>..HEAD -- <pkgDir>` 检测是否有提交
- 标记 `commitList`，用于 UI 提示 [有代码变动]

### 在发包流程中的感知

```tsx
const { userSelectedPkg } = await inquirer.prompt({
  type: 'list',
  name: 'userSelectedPkg',
  message: '请选择要发布的包',
  choices: diffPkgList.map(pkg => ({
    name: `${pkg.pkgName}${pkg.commitList?.length ? '[有代码变动]' : ''}${getDepsChange(pkg.deps) ? '[有依赖变动]' : ''}`,
    value: pkg,
  })),
})
```

- 用户界面显示哪些包有变动
- 发包时只针对选中的包操作
- 避免无意义发布


## 特点总结

- 自动化：无需手动查找包

- 感知代码变动：只发布有改动的包

- 感知依赖变动：依赖更新同步处理

- 支持 Monorepo：每个子包独立维护 CHANGELOG、版本号

- UI 友好：inquirer 界面提示 [有代码变动][有依赖变动]
