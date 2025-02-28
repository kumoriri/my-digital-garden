---
{"dg-publish":true,"permalink":"/gitignore/","updated":"2025-02-28T17:53:14.173+08:00"}
---

`.gitignore` 是一个用于 **告诉 Git 忽略某些文件或文件夹** 的配置文件。通过 `.gitignore`，你可以避免将不必要的文件（如临时文件、日志文件、IDE 配置文件等）提交到 Git 仓库中。以下是 `.gitignore` 的详细使用方法：

---

### **1. 创建 `.gitignore` 文件**
1. 在你的 Git 仓库根目录下创建一个名为 `.gitignore` 的文件。
2. 在文件中添加需要忽略的文件或文件夹的规则。

例如：
```bash
# 在终端中创建 .gitignore 文件
touch .gitignore
```

---

### **2. `.gitignore` 的语法规则**
`.gitignore` 文件支持以下语法规则：

#### **忽略特定文件**
直接写文件名：
```bash
# 忽略单个文件
file.txt
```

#### **忽略特定文件夹**
在文件夹名后加 `/`：
```bash
# 忽略整个文件夹
logs/
```

#### **忽略特定扩展名的文件**
使用通配符 `*`：
```bash
# 忽略所有 .log 文件
*.log
```

#### **忽略特定目录下的文件**
指定路径：
```bash
# 忽略 logs 文件夹下的所有 .log 文件
logs/*.log
```

#### **忽略特定文件，但不忽略子目录中的同名文件**
使用 `!` 排除：
```bash
# 忽略所有 .txt 文件，但不忽略 subdir/ 下的 .txt 文件
*.txt
!subdir/*.txt
```

#### **忽略所有文件，除了特定文件**
使用 `!` 排除：
```bash
# 忽略所有文件，但不忽略 file.txt
*
!file.txt
```

#### **注释**
以 `#` 开头的行是注释：
```bash
# 这是一个注释
```

---

### **3. 示例 `.gitignore` 文件**
以下是一个典型的 `.gitignore` 文件示例：
```bash
# 忽略所有 .log 文件
*.log

# 忽略 logs 文件夹
logs/

# 忽略 macOS 的 .DS_Store 文件
.DS_Store

# 忽略 Node.js 的 node_modules 文件夹
node_modules/

# 忽略 IDE 配置文件
.idea/
.vscode/

# 忽略编译生成的文件
build/
dist/

# 忽略本地环境配置文件
.env
```

---

### **4. 将 `.gitignore` 添加到 Git 仓库**
1. 创建 `.gitignore` 文件并添加规则。
2. 将 `.gitignore` 文件添加到 Git 仓库：
   ```bash
   git add .gitignore
   git commit -m "Add .gitignore file"
   ```

---

### **5. 忽略已提交的文件**
如果某些文件已经被提交到 Git 仓库，但你想忽略它们，可以按照以下步骤操作：

1. 从 Git 仓库中移除文件（但保留本地文件）：
   ```bash
   git rm --cached <file>
   ```
   例如：
   ```bash
   git rm --cached logs/error.log
   ```

2. 将文件添加到 `.gitignore` 中：
   ```bash
   echo "logs/error.log" >> .gitignore
   ```

3. 提交更改：
   ```bash
   git add .gitignore
   git commit -m "Ignore logs/error.log"
   ```

---

### **6. 全局 `.gitignore` 文件**
如果你想在所有 Git 仓库中忽略某些文件，可以设置全局 `.gitignore` 文件：
4. 创建全局 `.gitignore` 文件：
   ```bash
   touch ~/.gitignore_global
   ```
5. 添加规则到全局 `.gitignore` 文件：
   ```bash
   echo ".DS_Store" >> ~/.gitignore_global
   ```
6. 配置 Git 使用全局 `.gitignore` 文件：
   ```bash
   git config --global core.excludesfile ~/.gitignore_global
   ```

---

### **7. 检查 `.gitignore` 是否生效**
使用以下命令检查哪些文件会被 Git 忽略：
```bash
git status --ignored
```

---

### **总结**
- `.gitignore` 用于告诉 Git 忽略某些文件或文件夹。
- 语法规则包括通配符、路径、排除规则等。
- 如果文件已经被提交，需要使用 `git rm --cached` 移除。
- 可以设置全局 `.gitignore` 文件，适用于所有 Git 仓库。

如果还有其他问题，欢迎随时提问！ 😊