# Git 工作流说明 - 代码与帧数据分离管理

本项目使用**分支策略**来分离代码和帧数据的提交，让它们互不干扰。

## 分支说明

### 1. 代码分支（如 `main`, `frames_process` 等）
- **用途**：提交代码变更
- **特点**：`frames/` 目录被 `.gitignore` 忽略，不会出现在提交中
- **使用场景**：日常代码开发、bug修复、功能添加等

### 2. 帧数据分支（`frames-data`）
- **用途**：专门提交帧数据文件
- **特点**：`frames/` 目录**不被忽略**，可以正常提交
- **使用场景**：添加新的帧数据、更新现有帧数据等

## 使用方法

### 提交代码变更

```bash
# 1. 切换到代码分支（如 main 或 frames_process）
git checkout main  # 或你的代码分支名

# 2. 进行代码修改...

# 3. 提交代码（frames目录会被自动忽略）
git add .
git commit -m "feat: 添加新功能"
git push origin main
```

### 提交帧数据变更

```bash
# 1. 切换到帧数据分支
git checkout frames-data

# 2. 添加或修改帧数据文件...

# 3. 提交帧数据
git add frames/
git commit -m "data: 添加新的帧数据"
git push origin frames-data
```

### 查看帧数据

```bash
# 在代码分支中，虽然frames被忽略，但可以通过切换分支查看
git checkout frames-data
# 现在可以看到所有帧数据文件
```

## 注意事项

1. **分支切换**：在切换分支时，如果两个分支的 `.gitignore` 不同，Git 可能会提示一些文件的变化，这是正常的。

2. **合并策略**：通常不需要合并这两个分支，它们各自独立维护。

3. **远程仓库**：两个分支都可以推送到远程仓库，互不影响。

4. **首次设置**：如果 `frames-data` 分支还没有推送过，首次推送时使用：
   ```bash
   git push -u origin frames-data
   ```

## 当前分支状态

- **代码分支**：`.gitignore` 中包含 `frames/`，忽略帧数据
- **帧数据分支**：`.gitignore` 中注释掉了 `frames/`，可以跟踪帧数据

## 常见问题

**Q: 我在代码分支中修改了代码，也想更新帧数据，怎么办？**
A: 先提交代码，然后切换到 `frames-data` 分支提交帧数据。

**Q: 两个分支的代码会不同步吗？**
A: 不会。两个分支共享相同的代码，只是 `.gitignore` 的配置不同，所以对 `frames/` 目录的处理不同。

**Q: 如何查看帧数据分支的历史？**
A: 使用 `git log frames-data` 或切换到该分支后使用 `git log`。

