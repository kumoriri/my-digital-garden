---
{"dg-publish":true,"permalink":"/模版知识/Mac sips 调整文件大小/","tags":["garden"],"created":"2025-02-17T22:37:20.743+08:00","updated":"2025-03-17T21:37:40.862+08:00"}
---


在 Mac 上，`sips`（Scriptable Image Processing System）是一个强大的命令行工具，可以用来批量调整图片的大小、格式转换、颜色调整等。通过终端和 `sips` 命令，你可以编写简单的脚本，实现批量处理图片的功能。

以下是使用 `sips` 命令批量调整图片大小和格式的详细步骤：

---

### 1. 打开终端

在 Mac 上，打开 **“终端”** 应用程序（可以在 Launchpad 中搜索“终端”或通过 Spotlight 找到）。

---

### 2. 创建一个批量处理脚本

你可以在终端中直接编写脚本，也可以使用文本编辑器（如 VSCode、Sublime Text 或自带的 TextEdit）编写脚本并保存为 `.sh` 文件。

#### 示例：批量调整图片大小并转换格式

以下是一个简单的脚本示例，它会：

1. 将指定文件夹中的所有图片调整为宽度为 1024 像素（保持纵横比）。
    
2. 将图片格式转换为 JPEG，并保存到一个新的文件夹中。
    

bash复制

```bash
#!/bin/bash

# 定义源文件夹和目标文件夹
SOURCE_FOLDER="~/Desktop/source_images"  # 源图片所在的文件夹
TARGET_FOLDER="~/Desktop/resized_images" # 调整大小后的图片保存的文件夹

# 创建目标文件夹（如果不存在）
mkdir -p "$TARGET_FOLDER"

# 遍历源文件夹中的所有图片
for image in "$SOURCE_FOLDER"/*; do
    if [[ -f "$image" ]]; then  # 确保是文件
        # 获取文件名和扩展名
        filename=$(basename "$image")
        extension="${filename##*.}"
        filename="${filename%.*}"

        # 调整图片大小并转换为 JPEG 格式
        sips -Z 1024 --out "${TARGET_FOLDER}/${filename}.jpg" "$image"

        echo "Processed: $filename"
    fi
done

echo "All images have been resized and saved to $TARGET_FOLDER"
```

---

### 3. 保存脚本并运行

1. 将上述脚本保存为一个文件，例如 `resize_images.sh`。
    
2. 打开终端，导航到脚本所在的目录：
    
    bash复制
    
    ```bash
    cd /path/to/your/script
    ```
    
3. 给脚本文件添加可执行权限：
    
    bash复制
    
    ```bash
    chmod +x resize_images.sh
    ```
    
4. 运行脚本：
    
    bash复制
    
    ```bash
    ./resize_images.sh
    ```
    

---

### 4. 脚本说明

- `SOURCE_FOLDER` 和 `TARGET_FOLDER` 是你定义的源文件夹和目标文件夹路径。
    
- `sips -Z 1024`：将图片的最大尺寸调整为 1024 像素（宽度或高度），并保持纵横比。
    
- `--out`：指定输出文件的路径和格式。
    
- `*`：匹配文件夹中的所有文件。
    
- `[[ -f "$image" ]]`：确保当前项是文件，而不是文件夹。
    

---

### 5. 其他 `sips` 命令选项

- **调整图片大小**：
    
    bash复制
    
    ```bash
    sips -Z <size> --out <output_file> <input_file>
    ```
    
    - `-Z <size>`：设置图片的最大尺寸（宽度或高度）。
        
- **转换图片格式**：
    
    bash复制
    
    ```bash
    sips --out <output_file> <input_file>
    ```
    
    - 输出文件的扩展名决定了格式（如 `.jpg`、`.png`）。
        
- **调整图片颜色**：
    
    bash复制
    
    ```bash
    sips -s format jpeg -s formatOptions 75 --out <output_file> <input_file>
    ```
    
    - `-s formatOptions`：设置图片质量（0-100）。
        

---

### 6. 示例：批量转换格式

如果你想批量将图片从 PNG 转换为 JPEG，可以使用以下脚本：

bash复制

```bash
#!/bin/bash

SOURCE_FOLDER="~/Desktop/source_images"
TARGET_FOLDER="~/Desktop/converted_images"

mkdir -p "$TARGET_FOLDER"

for image in "$SOURCE_FOLDER"/*.png; do
    if [[ -f "$image" ]]; then
        filename=$(basename "$image")
        filename="${filename%.*}"

        sips --out "${TARGET_FOLDER}/${filename}.jpg" "$image"
        echo "Converted: $filename"
    fi
done

echo "All images have been converted to JPEG format."
```

---

### 总结

通过终端和 `sips` 命令，你可以轻松实现批量调整图片大小、转换格式等操作。这种方式非常适合需要自动化处理大量图片的场景。你可以根据需求修改脚本，调整参数以满足不同的处理需求。