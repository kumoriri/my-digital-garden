---
{"dg-publish":true,"permalink":"/00 Test/Git/DS_Store/","tags":["garden"],"updated":"2025-04-14T19:40:12.770+08:00"}
---


`.DS_Store` 文件是 **macOS 操作系统自动生成**的隐藏文件，用于存储文件夹的自定义视图设置（如图标位置、窗口大小、背景图片等）。以下是关于它的详细说明和常见处理方法：

---

### **1. 什么是 `.DS_Store`？**
- **全称**：Desktop Services Store。
- **作用**：保存当前文件夹的显示配置（例如图标的排列方式、窗口位置等），帮助 macOS 记住用户的个性化设置。
- **生成位置**：每个文件夹中可能都会生成一个 `.DS_Store` 文件。
- **隐藏性**：在 macOS 的 Finder 中默认不可见（隐藏文件）。

---

### **2. 为什么 `.DS_Store` 可能带来问题？**
- **跨平台协作**：如果通过 Git、U盘或云端共享文件夹，Windows/Linux 用户可能会看到这些文件，造成干扰。
- **版本控制污染**：Git 仓库中可能误提交 `.DS_Store`，导致仓库臃肿。
- **潜在敏感信息**：某些情况下，文件夹名称或结构可能通过 `.DS_Store` 泄露。

---

### **3. 如何避免或处理 `.DS_Store` 文件？**

#### **方法 1：禁止 macOS 生成 `.DS_Store`**
通过终端命令全局禁用生成：
```bash
# 禁止在本地磁盘生成
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true

# 禁止在网络驱动器（如共享文件夹）生成
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
```
重启电脑后生效。  
（注意：此操作可能影响 Finder 的个性化功能。）

#### **方法 2：删除现有 `.DS_Store` 文件**
在终端中递归删除所有 `.DS_Store` 文件：
```bash
# 删除当前目录及子目录下的所有 .DS_Store
find . -name ".DS_Store" -type f -delete
```

#### **方法 3：在 Git 中忽略 `.DS_Store`**
在项目的 `.gitignore` 文件中添加规则：
```bash
# 在 .gitignore 文件中添加以下内容
**/.DS_Store
```
若已提交到仓库，需从 Git 记录中彻底删除：
```bash
git rm --cached **/.DS_Store
git commit -m "Remove .DS_Store files"
```

#### **方法 4：使用清理工具（推荐）**
- **BlueHarvest**：自动删除 macOS 生成的临时文件（如 `.DS_Store`）。
- **CleanMyMac**：提供系统清理功能，可批量删除此类文件。

---

### **4. 如何查看隐藏的 `.DS_Store` 文件？**
在 macOS 的 Finder 中临时显示隐藏文件：
```bash
# 显示隐藏文件
defaults write com.apple.finder AppleShowAllFiles -boolean true
killall Finder

# 恢复隐藏
defaults write com.apple.finder AppleShowAllFiles -boolean false
killall Finder
```

---

### **总结**
- **普通用户**：无需主动操作，但共享文件前可删除 `.DS_Store`。
- **开发者**：通过 `.gitignore` 永久忽略此类文件，避免污染仓库。
- **强迫症患者**：使用工具或脚本定期清理。

如果还有其他疑问，欢迎随时提问！ 😊