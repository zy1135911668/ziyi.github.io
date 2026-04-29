---
name: image-recognition
description: "支持图片内容识别与分析：识别图内物体、人物、文字、场景、情感，以及从截图中提取结构化信息。"
homepage: https://docs.openclaw.ai/tools/image
metadata:
  {
    "openclaw":
      {
        "emoji": "🖼️",
        "requires": {},
        "install":
          [
            {
              "id": "config",
              "kind": "config",
              "label": "配置 vision 模型 (如 OpenAI gpt-4o-mini)",
            },
            {
              "id": "sharp",
              "kind": "npm",
              "label": "安装 sharp 图片处理模块（可选依赖）",
            },
          ],
      },
  }
---

# 图片识别 Skill

识别和分析图片内容，提取结构化信息。

## 触发场景

✅ **使用这个 skill 当用户：**

- 发送图片询问"这是什么动物/植物/建筑？"
- "帮我看看这张图里的文字"
- "这张截图里有什么信息？"
- "分析这张图表的数据"
- "这张照片是在哪里拍的？"
- "描述这张图片"
- "给这张图写个说明"

## 禁用场景

❌ **不要使用当：**

- 用户问关于视频内容（图片识别不支持视频帧分析）
- 需要 OCR 精确到像素级别的文字提取
- 图片包含恶意或隐私敏感内容 → 应先询问用户确认
- 医学影像诊断或 X 光分析
- 用户上传文件而非图片

## 使用方法

### 基础图片识别

使用 `image` 工具，传入图片路径或 URL，配合 prompt 描述需要分析的内容。

```
# 通用图片描述
描述这张图片

# 特定分析
这张图里有什么文字/物体/人物？
这张照片的色调和氛围如何？
帮我从这张截图里提取信息
```

### 参数说明

| 参数 | 说明 | 推荐值 |
|------|------|--------|
| prompt | 分析指令，越具体越好 | "描述图中文字"、"识别这个植物" |
| model | 视觉模型（可选） | 默认使用配置的 imageModel |
| maxBytesMb | 图片大小上限 | 默认 20MB |
| maxImages | 一次最多分析的图片数 | 默认 20 张 |

### 图片格式支持

- JPEG (.jpg, .jpeg)
- PNG (.png)  
- GIF (.gif) — 只分析第一帧
- WebP (.webp)
- BMP (.bmp)

## 快速示例

**"这张图片里有什么？"**
```
image(prompt="详细描述这张图片里的所有元素")
```

**"帮我读一下这张截图上的文字"**
```
image(prompt="提取这张图片中的所有文字信息，按顺序列出")
```

**"这张图里有什么异常吗？"**
```
image(prompt="检查这张图片，找出任何不寻常或值得注意的元素")
```

## 配置说明

1. 需要一个支持 vision 的模型（如 OpenAI gpt-4o-mini）
2. 确保 OpenClaw 已正确配置 `agents.defaults.imageModel`
3. 安装可选依赖 `sharp` 以优化图片处理：

```bash
cd %APPDATA%/npm/node_modules/openclaw
npm install sharp
```

## 注意事项

- 图片识别质量取决于配置的视觉模型能力
- 图片过大会被自动压缩优化以节省 token
- 不支持视频流实时分析
- 识别结果的准确性受图片清晰度影响
- 建议在上传前对敏感图片做脱敏处理
