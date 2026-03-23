# 图片生成指南

## 支持的模型

### 文生图模型
- **nano-banana** - 标准图片生成模型（费用 0.08）；文生图/图生图/多图参考；参考图支持 `b64/URL/data:image/*`
- **nano-banana-hd** - 4K 高清版本（费用 0.12）；文生图/图生图/多图参考；参考图支持 `b64/URL/data:image/*`
- **nano-banana-2** - BANANA2 直返图模型（费用 0.2）
- **nano-banana-2-2K** - BANANA2 2K 直返图模型（费用 0.2）
- **nano-banana-2-4k** - BANANA2 4K 直返图模型（费用 0.2）
- **nano-banana-pro** - BANANA2 Pro 直返图模型（费用 0.2）
- **gemini-2.5-flash-image** - Gemini 2.5 Flash 绘图模型（费用 0.04）
- **gemini-2.5-flash-image-preview** - Gemini 2.5 Flash 预览版（费用 0.04）
- **gemini-3.1-flash-image-preview** - Gemini 3.1 Flash 图像预览（费用 0.1）
- **gemini-3.1-flash-image-preview-2k** - Gemini 3.1 Flash 2K 图像预览（费用 0.1）
- **gemini-3.1-flash-image-preview-4k** - Gemini 3.1 Flash 4K 图像预览（费用 0.1）

> 说明：`gemini-2.5-flash-image*` / `gemini-3.1-flash-image-preview*` 可用于文生图与图编辑场景，通常会先返回链接（本脚本会自动下载落地为图片文件）。
> 价格参考：`gemini-2.5-*` 约 0.04/张；`gemini-3.1-*` 约 0.1/张；直返图 BANANA2 约 0.2/张。
> 参考图输入支持：文件路径、`http(s)` URL、`data:image/*`、以及 `b64:<base64>`（最多 14 张）。

### 图生图模型
- **nano-banana-edit** - 图生图/多图参考（费用 0.08）；直接返图
- **nano-banana-2 / nano-banana-2-2K / nano-banana-2-4k / nano-banana-pro** - 支持图生图编辑（直返图，费用 0.2）
- **gemini-2.5-flash-image* / gemini-3.1-flash-image-preview*** - 支持多图组合编辑（最多 14 张）

## 图片比例选项

- `4:3` - 横屏比例（推荐）
- `3:4` - 竖屏比例
- `16:9` - 宽屏比例
- `9:16` - 手机屏比例
- `2:3` - 竖屏比例
- `3:2` - 横屏比例

## 使用流程

### 文生图

1. **选择模型** - 根据需求选择合适的模型
2. **输入提示词** - 详细描述您想要的图片内容
3. **选择比例** - 根据用途选择合适的长宽比
4. **生成图片** - 等待 AI 处理完成

### 图生图

1. **上传参考图片** - 选择一张参考图片
2. **输入提示词** - 描述您想要的修改或效果
3. **生成图片** - 等待 AI 处理完成

### 多图组合（最多 14 张）

- 可通过 `--images` 传入逗号分隔的多图引用（路径/URL/data/b64），支持最多 14 张图组合生成新图
- 也可与 `--image` 一起使用（内部统一合并处理）

## 提示词技巧

### 描述主体
- 人物、动物、物体等主要元素

### 添加风格
- 写实、卡通、油画、水彩、科幻等

### 指定场景
- 室内、户外、特定地点、背景环境

### 描述光线
- 明亮、昏暗、夕阳、月光、自然光等

### 添加情感
- 快乐、神秘、温馨、科幻、浪漫等

## 示例

### 文生图示例

```bash
python3 {baseDir}/scripts/wangyi-banana.py \
  --task text-to-image \
  --prompt "一只可爱的橘猫坐在窗台上，阳光透过窗户洒在它身上，写实风格，4K高清" \
  --model nano-banana \
  --aspect-ratio 4:3 \
  -o /tmp/openclaw/wangyi-output/cat.png
```

### 图生图示例

```bash
python3 {baseDir}/scripts/wangyi-banana.py \
  --task image-to-image \
  --prompt "将背景改为夜晚，添加星空" \
  --image /path/to/image.png \
  --model nano-banana-edit \
  -o /tmp/openclaw/wangyi-output/edited.png
```

## 注意事项

- 图片生成通常需要 10-30 秒
- 高清模型生成时间可能更长
- 提示词越详细，生成效果越好
- 支持多种图片格式输出（PNG, JPG 等）
