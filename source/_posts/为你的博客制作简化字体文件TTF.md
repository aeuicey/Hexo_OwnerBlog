---
abbrlink: ''
categories:
- - 技术
date: '2025-08-27T19:47:52.163024+08:00'
tags:
- 简化字体
- 博客优化
title: 为你的博客制作简化字体文件TTF
updated: '2025-08-27T19:47:52.711+08:00'
---
# 为你的博客制作简化字体文件TTF - Alice Blog

> ## Excerpt
>
> 一个个人兴趣驱动的blog

---

## **[![](https://www.alicetec.cn/upload/XY-221116-Smiley-Sans-10_%E7%BB%93%E6%9E%9C.webp)](https://www.alicetec.cn/upload/XY-221116-Smiley-Sans-10_%E7%BB%93%E6%9E%9C.webp)通过指定 Unicode 范围裁剪 TTF 字体文件**

最近尝试为博客添加自定义字体，以在不同的浏览器上实现视觉一致性。你可能已经了解了 `@font-face` 这个 CSS 属性：

```css
@font-face { font-family: "FontName"; src: url("/assets/FontFile.ttf"); }
```

但是在某些特定情况下，我们只需要字体文件的一小部分（英文字母或某些特殊符号），但是字体创建者没有提供小字体集版本。这些小字集在优化比克加载性能上有这至关重要的作用。

## **简易方法**

我们可以使用 Python [fontTools](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fgithub.com%2Ffonttools%2Ffonttools) 库手动减少字体文件大小，这个工具专注于合并、裁剪子集和转换字体文件。对于减小字体文件大小的场景，可以使用这个库提供的 `pyftsubset` 命令，最简单的方法是：

```graphql
# 安装 fonttools，我使用的是 4.32.0 版本。 pip install fonttools pyftsubset Input.ttf --output-file=Output.ttf --unicodes=U+0000-007F
```

两个基本的参数含义分别为：

`--output-file=`：输出文件名。

`--unicodes=`：以十六进制数字指定 Unicode 范围。比如 `U+0000-0007F` 表示 ASCII 码。

要查看更多选项，请访问 [https://fonttools.readthedocs.io/en/latest/subset/index.html](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Ffonttools.readthedocs.io%2Fen%2Flatest%2Fsubset%2Findex.html)。

## **实用小脚本版本 2（23.10.25 更新）**

下方的脚本补充了更丰富的参数，使用方法同版本 1，区别在于可以保留 Features 和一些必要的扩展字符集合等等，最终文件会略大一些。如果只是简易的裁剪，仍然推荐使用版本 1。

```bash
#!/bin/bash if [[ $# -lt 1 || !($1 == *.otf || $1 == *.ttf) ]]; then echo "Use VENV: source ./env/bin/activate" echo "Usage: subascii <fontfile.otf/ttf> [pyftsubset options...]" exit 1 fi filename=$(basename -- "$1") extension="${filename##*.}" filename="${filename%.*}" pyftsubset "$1" --output-file="${filename}-Sub.${extension}" --unicodes="U+0000-007F" "${@:2}" \ --layout-features='*' --glyph-names --symbol-cmap --legacy-cmap \ --notdef-glyph --notdef-outline --recommended-glyphs \ --name-IDs='*' --name-legacy --name-languages='*'
```

## **实用小脚本版本 1（2023.07.26 更新）**

分享一个小脚本，要求已经安装`fonttools`，运行后会产生一个 ASCII 子集的新文件，文件名结尾加`-Sub`

用法举例：`./subascii.sh Rubik.ttf` 得到 `Rubik-sub.ttf`

下面的保存为`subascii.sh`

```bash
#!/bin/bash if [[ $# -lt 1 || !($1 == *.otf || $1 == *.ttf) ]]; then echo "Use VENV: source ./env/bin/activate" echo "Usage: subascii <fontfile.otf/ttf> [pyftsubset options...]" exit 1 fi filename=$(basename -- "$1") extension="${filename##*.}" filename="${filename%.*}" pyftsubset "$1" --output-file="${filename}-Sub.${extension}" --unicodes=U+0000-007F "${@:2}"
```

这个结果可能没有实际意义，因为它取决于指定的 Unicode 范围大小，以及具体参数配置。以下是基于 `RobotoCondensed-Bold.ttf` 裁剪后的比对。

```css
Input.ttf 162K Output.ttf 22K
```

## 在Windows上运行简单脚本

**基于以上bash，笔者还给出了cmd/bat版本使用**

```bash
@echo off setlocal enabledelayedexpansion if "%~1"=="" ( echo Use VENV: .\env\Scripts\activate echo Usage: subascii.bat ^<fontfile.otf/ttf^> [pyftsubset options...] exit /b 1 ) set "fullname=%~nx1" set "filename=%~n1" set "extension=%~x1" if /i not "%extension%"==".otf" if /i not "%extension%"==".ttf" ( echo Use VENV: .\env\Scripts\activate echo Usage: subascii.bat ^<fontfile.otf/ttf^> [pyftsubset options...] exit /b 1 ) :: 添加 --ignore-missing-glyphs 选项 pyftsubset "%~1" --output-file="%filename%-Sub%extension%" --unicodes=U+0000-007F --ignore-missing-glyphs %*
```

需要注意的是，为了方便使用添加 了`--ignore-missing-glyphs` 选项，这样在遇到缺失的字形时就不会报错。

### **功能概述**

此脚本用于创建 OTF 或 TTF 字体文件的 ASCII 子集，生成的新字体仅包含基本 ASCII 字符（U+0000 - U+007F），有助于减小字体文件大小。

### **使用前提**

1. **Python 环境**：需要安装 Python 并配置好环境变量，一般来说pip自带
2. **Fonttools 库**：需提前安装 fonttools（通过 `pip install fonttools` 安装）

### **基本用法**

```batch
subascii.bat <字体文件.otf/ttf> [pyftsubset 选项...]
```

- **必选参数**：

  - `<字体文件.otf/ttf>`：指定要处理的字体文件路径（需为 OTF 或 TTF 格式）
- **可选参数**：

  - `[pyftsubset 选项...]`：传递给 `pyftsubset` 命令的额外参数（例如：`--desubroutinize`、`--with-zopfli` 等）

### **使用示例**

**简单处理**：

```batch
subascii.bat C:\Fonts\SourceHanSans-Regular.otf
```

- 输出文件：`SourceHanSans-Regular-Sub.otf`

**带额外选项**：

```batch
subascii.bat C:\Fonts\Roboto-Regular.ttf --desubroutinize --with-zopfli
```

- 输出文件：`Roboto-Regular-Sub.ttf`
- 同时应用了额外的优化选项

### **输出说明**

- 脚本会在原字体文件所在目录生成新文件，文件名格式为 `原文件名-Sub.原扩展名`
- 生成的字体仅包含 ASCII 字符集（0-127 编码范围）

### **注意事项**

1. **文件路径**：若字体文件路径包含空格，需用双引号包裹整个路径，所以说尽量不要使用空格路径
2. **权限问题**：确保对输出目录有写入权限，尤其是服务器系统
3. **参数传递**：额外选项会直接传递给 `pyftsubset`，请参考[https://fonttools.readthedocs.io/en/latest/subset/index.html](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Ffonttools.readthedocs.io%2Fen%2Flatest%2Fsubset%2Findex.html) 获取可用选项列表

## **在哪里找到字体文件？**

**注意**，字体并不总是被允许修改，请仔细查看字体使用许可证。

- [http://fonts.google.com/](http://fonts.google.com/)
- [https://fonts.adobe.com/](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Ffonts.adobe.com%2F)
- [https://fonts.zeoseven.com/](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Ffonts.zeoseven.com%2F)
- [https://drxie.github.io/OSFCC/](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fdrxie.github.io%2FOSFCC%2F)

## **在哪里找到 Unicode 编码？**

- [http://www.unicode.org/charts/](http://www.unicode.org/charts/)
- [https://unicodelookup.com/](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Funicodelookup.com%2F)

## 参考文献（包含引用、修改与工程实例）

1. [https://github.com/HACKERSam2011/NanoFullSong](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fgithub.com%2FHACKERSam2011%2FNanoFullSong)
2. [https://roger.zone/post/reduce-ttf-font-file-size-using-python/](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Froger.zone%2Fpost%2Freduce-ttf-font-file-size-using-python%2F)
3. [https://fontsmaller.github.io/](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Ffontsmaller.github.io%2F)
4. [「译文」网页字体性能探讨-你的字体是如何影响网页速度的 - 知乎](https://www.alicetec.cn/linkJump?target=https%3A%2F%2Fzhuanlan.zhihu.com%2Fp%2F338787317)
