# 游戏资源

把图片、音频、JSON 等运行时资源放在本目录，通过 `assetUrl('relative/path')` 获取部署地址。

`images/boost.png`：用户提供的加速双箭头 PNG，原文件直接复制，用于游戏加速按钮；状态着色由 Phaser 运行时处理。

`audio/{eat,boost,death}.wav`：本项目原创程序合成的短提示音，无第三方采样，可随项目分发。运行 `node apps/serpent-run/scripts/generate-audio.mjs` 可确定性重新生成；22050 Hz、单声道 PCM16，总体积约 29 KB。属于试玩音效，正式听感及手机扬声器表现待验收。

`images/cartoon-mascot.png`：2026-09-22 使用内置 imagegen，以用户确认的五屏卡通概念图为风格参考生成的透明蛇蛇插画；用于首页的装饰，不参与碰撞。无外部下载素材。提示词要点：大眼睛绿色蛇、奶油色腹部、糖果高光、深绿描边、追逐金色能量豆、透明背景、无文字。概念图不是运行时整屏贴图，控件、分数和状态均由 Phaser 实时绘制。

`docs/design/serpent-run/cartoon-result-v1.png`（仓库根目录下）：同日使用内置 imagegen 基于上述蛇蛇形象生成的结算表情，提示词要点：保持同一身份与画风、盘起身体、眩晕叉叉眼、吐舌、透明背景、无文字。该版已移出发布资源目录，保留为设计迭代来源，当前不再预加载。

2026-09-22 对照用户提供的五屏设计指引，使用内置 imagegen 补充以下素材，均无文字、无外部下载素材：

- `images/cartoon-ready.png`：透明站立小蛇，奶油腹部、圆润大眼、短卷尾与金色小光芒，用于开局面板上沿。
- `images/cartoon-result-wide.png`：透明横向趴倒小蛇，保留叉叉眼、吐舌和眩晕线，匹配结算卡片顶部横向构图。
- `images/cartoon-backdrop.png`：薄荷天空、奶油渐变、圆云和边缘热带叶片的竖屏背景；首页、设置和结算共用，控件仍实时绘制。

生成源文件保存在 Codex 当前任务的 generated_images 目录；运行时副本统一在本目录并经 manifest 注册。运行时资源继续受仓库 8 MiB 预算约束。

## 首页新版图标

2026-09-22 使用内置 imagegen 分别生成六枚透明糖果图标：

- [开始：糖果小屋](images/candy-icon-home.webp)
- [加成：能量糖](images/candy-icon-boost.webp)
- [商城：糖果袋](images/candy-icon-shop.webp)
- [排行：奖杯](images/candy-icon-rank.webp)
- [任务：任务卡](images/candy-icon-quest.webp)
- [设置：齿轮](images/candy-icon-settings.webp)

生成 PNG 原稿保留在 Codex 当前任务 generated_images 中；运行时文件仅进行无损 WebP 编码，未裁切、缩放或改画。逐像素核对所有可见 RGB 与完整 alpha 一致。六枚图标合计约 4.1 MiB；淘汰的结算旧图移入 docs/design，避免随构建重复发布。完整生成提示词见 [图标提示词](../../../../docs/design/serpent-run/candy-icons-prompts.md)。

`images/gesture-{drag,hold}.svg`：原创代码绘制的透明矢量操作插画，取代旧 Graphics 拼块手指。两者共用奶油手套、薄荷袖口和柔和高光；拖动用双向箭头，长按用金色按压光圈及闪电徽记。SVG 以 384×384 栅格化后在开局显示为 88×88，统一经 manifest 加载，无外部字体或素材。
