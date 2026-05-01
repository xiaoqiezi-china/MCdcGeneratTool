# Minecraft 物品组件生成器 | Item Component Builder
/////////唯一一段人写的话/////////////
整个项目包括README.me全部由DeepseekV4-flash模型完成。截止花费2.5元
deepseek王朝了。
////////////////////////////////////






> **Minecraft 1.21.1** 物品组件可视化编辑器 — 通过直观的图形界面生成 `/give` 命令与物品组件 JSON。

![Version](https://img.shields.io/badge/Minecraft-1.21.1-green?style=flat-square)
![Size](https://img.shields.io/badge/size-single%20file-important?style=flat-square)
![Language](https://img.shields.io/badge/vanilla%20JS-no%20dependencies-brightgreen?style=flat-square)

---

## 概述

这是一个**纯前端、单文件**的 Web 应用，为 Minecraft 1.21.1 的物品组件系统提供可视化编辑界面。无需任何构建工具或服务端，在浏览器中打开即可使用。

通过拖拽式面板为物品添加各类组件（属性修饰符、附魔、药水效果、容器内容等），实时生成对应的 `/give` 命令或物品组件 JSON，可直接用于数据包或命令方块。

---

## 功能特色

- **可视化组件编辑** — 按分类（基础/战斗/功能/容器/信息/装饰/实体/特殊）浏览并添加 40+ 种物品组件
- **实时输出** — 右侧面板同步显示 `/give` 命令和 `item_stack` JSON，支持一键复制与导出
- **拖拽排序** — 已添加的组件可拖拽调整顺序
- **富文本名称** — 内置 § 颜色代码编辑器，支持 Minecraft JSON 文本组件格式
- **智能序列化** — 自动处理组件间的依赖与冲突，生成符合 1.21.1 格式的输出
- **暗色 Minecraft 风格 UI** — 仿 minecraft.net 配色方案，像素风字体
- **纯离线可用** — 单 HTML 文件，无任何外部依赖

---

## 快速开始

### 方式一：直接打开

用浏览器直接打开 `index.html` 即可，无需任何服务端（部分浏览器可能限制本地 `file://` 下的剪贴板 API）。

### 方式二：通过 HTTP 服务（推荐）

使用 Python 启动本地服务器：

```bash
cd G:/项目/mc-item-builder
python -m http.server 8080 --bind 127.0.0.1
```

然后访问 [http://127.0.0.1:8080](http://127.0.0.1:8080)

> 通过 HTTP 访问时可正常使用「复制到剪贴板」功能。

---

## 使用指南

### 基本流程

1. **选择基础物品** — 在左侧面板选择目标物品（如 `minecraft:diamond_sword`），设置数量与 Count
2. **添加组件** — 从左侧调色板点击组件上的 `+` 按钮添加
3. **配置参数** — 在中间工作区编辑各组件的详细参数
4. **获取输出** — 右侧面板实时生成 `/give` 命令或 JSON，点击「复制」即可使用

### 组件分类

| 分类 | 说明 | 示例组件 |
|------|------|---------|
| 📋 基础信息 | 物品基本属性 | 名称、描述、附魔光效、无法破坏 |
| ⚔️ 战斗属性 | 战斗相关 | 攻击伤害、攻击速度、护甲值 |
| 🔧 功能 | 功能性组件 | 食物、工具、修复、消耗品 |
| 📦 容器 | 容器内容 | 物品栏、储物箱内容、烟火属性 |
| ℹ️ 信息 | 物品信息 | 隐藏标签、属性修饰符 |
| 🎨 装饰 | 外观装饰 | 火焰弹颜色、染料颜色、旗帜图案、盔甲纹饰 |
| 👾 实体 | 实体相关 | 怪物放置实体、方块实体数据 |
| ⭐ 特殊 | 特殊组件 | 药水效果、音效、 creature 等 |

### 输出格式

- **命令模式** — 生成完整的 `/give @p ...` 命令，含组件 JSON
- **JSON 模式** — 仅生成 `item_stack` 的 components JSON 片段
- 支持导出为 `.mcfunction` 或 `.json` 文件

### 富文本编辑器

在需要输入名称或描述文本的组件中，点击输入框会弹出富文本编辑器：
- 添加多个文本段，每段可独立设置颜色
- 支持格式标记：**粗体**、*斜体*、~~删除线~~、下划线
- 实时预览最终显示效果

---

## 技术栈

| 技术 | 说明 |
|------|------|
| **HTML5** | 语义化结构，三栏布局 |
| **CSS3** | 原生变量（Custom Properties）、Flexbox、暗色主题 |
| **Vanilla JavaScript** | ES6+，无框架无依赖 |
| **设计模式** | 类 MVC 架构：数据定义 → 状态管理 → 渲染 → 输出序列化 |
| **字体** | Minecraft AE Pixel / Minecraft AE（系统安装后使用，否则回退到 monospace） |

整个应用仅为一个 `index.html` 文件（约 96KB），内部以内联 `<style>` 和 `<script>` 组织，零外部请求。

---

## 项目结构

```
G:/项目/
├── mc-item-builder/           # 主项目（当前目录）
│   └── index.html             # 单文件应用 (~96KB)
├── mc-item-builder-backup/    # 旧版本备份
│   ├── index.html
│   └── index.html.bak-*
├── minecraftweb/              # Minecraft 官网快照（minecraft.net 存档）
│   ├── index.html
│   └── assets/
│       ├── images/
│       ├── style_1.css
│       ├── style_2.css
│       └── ...
├── .claude/
│   └── settings.local.json
└── CLAUDE.md                  # Claude Code 项目说明
```

### index.html 内部结构

| 区域 | 说明 |
|------|------|
| **CSS `<style>`** | Minecraft 暗色主题，三栏布局，响应式适配，1900+ 行 |
| **左侧面板 (Palette)** | 8 个分类选项卡，组件列表，`+` 添加按钮 |
| **中间工作区 (Workspace)** | 基础物品设置 + 已添加组件列表，拖拽排序，禁用/删除 |
| **右侧输出 (Output)** | 命令/JSON 切换，复制按钮，字符计数，导出下载 |
| **JS 数据定义** | `CATEGORIES`, `ENCHANTS`, `POTIONS`, `EFFECTS`, `ATTRIBUTES`, `COMPONENT_DEFS` 等 |
| **JS 状态管理** | `workspaceBlocks[]` 组件状态数组 |
| **JS 渲染** | `renderPalette()`, `renderWorkspace()` 全量重绘 |
| **JS 输出** | `generateOutput()` → `buildComponentsJSON()` → `buildGiveCommand()` |

---

## 已支持的组件（40+）

| 组件 ID | 名称 | 分类 | 参数 |
|---------|------|------|------|
| `item_name` | 基础名称(非斜体) | basic | 富文本名称 |
| `custom_name` | 自定义名称(斜体) | basic | 富文本名称 |
| `lore` | 物品描述 | basic | 富文本描述行 |
| `enchantments` | 附魔 | basic | 附魔 ID + 等级多组 |
| `stored_enchantments` | 存储附魔 | basic | 附魔 ID + 等级多组（附魔书专用） |
| `dyed_color` | 染色 | deco | RGB 颜色 |
| `glider` | 鞘翅滑翔 | basic | 布尔开/关 |
| `firework_shapes` | 烟花形状 | container | 形状枚举 |
| `firework_explosion` | 烟火爆炸 | container | 颜色、褪色、形状、效果 |
| `fireworks` | 烟花属性 | container | 飞行时长、爆炸列表 |
| `instrument` | 山羊角音色 | basic | 音色枚举 |
| `map_color` | 地图颜色 | basic | 十六进制颜色 |
| `trim` | 盔甲纹饰 | deco | 材料 + 图案 |
| `unbreakable` | 无法破坏 | basic | 布尔开/关（显示为假） |
| `attribute_modifiers` | 属性修饰符 | combat | 属性 + 名称 + 值 + 操作 + 槽位 + 显示 |
| `damage` | 攻击伤害 | combat | 数值 |
| `max_damage` | 最大耐久 | basic | 数值 |
| `max_stack_size` | 最大堆叠 | basic | 数值 |
| `rarity` | 稀有度 | basic | 枚举 |
| `repair_cost` | 修复花费 | utility | 数值 |
| `tool` | 工具属性 | utility | 挖掘速度、规则列表 |
| `food` | 食物 | utility | 饥饿值、饱和度、是否可食用、效果列表 |
| `consumable` | 消耗品 | utility | 消耗音效、动画 |
| `use_remainder` | 使用残留物 | utility | 残留物品 ID |
| `use_cooldown` | 使用冷却 | utility | 秒数、冷却组 |
| `jukebox_playable` | 唱片机播放 | deco | 曲目 |
| `lock` | 物品锁 | container | 钥匙物品谓词 |
| `container` | 容器内容 | container | 物品栏列表 |
| `banner_patterns` | 旗帜图案 | deco | 图案 + 颜色多组 |
| `potions` | 药水效果(状态) | special | 效果 ID + 持续时间 + 放大器 |
| `potion_contents` | 药水内容物 | special | 药水 + 自定义效果列表 |
| `charged_projectiles` | 已装填抛射物 | container | 物品列表 |
| `intangible_projectile` | 无形抛射物 | entity | 布尔开/关 |
| `entity_data` | 实体数据 | entity | 实体类型 + NBT 数据（JSON） |
| `bundle_contents` | 束包内容 | container | 物品列表 |
| `hide_tooltip` | 隐藏提示框 | info | 布尔开/关 |
| `hide_additional_tip` | 隐藏额外信息 | info | 布尔开/关 |
| `note_block_sound` | 音符盒音效 | deco | 音效枚举 |
| `enchantment_glint` | 附魔光效 | basic | 布尔开/关 |
| `equippable` | 可穿戴 | entity | 槽位、音效、模型 |
| `writable_book_content` | 可写书内容 | container | 页面列表 |
| `written_book_content` | 成书内容 | container | 标题、作者、页面列表 |
| `ominous_bottle_amplifier` | 不祥之瓶放大器 | utility | 放大器等级 |
| `custom_data` | 自定义标签 | special | 任意 NBT JSON |
| `weapon` | 武器属性 | combat |  ranged_damage + 跨度和速度乘数 |
| `repairable` | 可修复 | utility | 修复材料列表 |
| `death_protection` | 死亡保护 | utility | 布尔开/关 |
| `block_state` | 方块状态 | basic | 属性键值对列表 |
| `container_loot` | 容器战利品 | container | 战利品表 + 种子 |
| `recipes` | 配方 | info | 配方 ID 列表 |
| `creative_slot_lock` | 创造模式槽锁定 | special | 布尔开/关 |

---

## 自定义与扩展

### 添加新组件

在 `COMPONENT_DEFS` 对象中添加条目：

```js
example_component: {
  id: 'example_component',
  name: '示例组件',
  category: 'basic',       // 属于哪个分类
  icon: '✨',
  desc: '组件说明文字',
  params: [
    { type: 'text', key: 'value', label: '文本值', default: '' },
    { type: 'number', key: 'count', label: '数量', default: 1 },
    { type: 'checkbox', key: 'flag', label: '开关', default: false },
  ],
  toJSON(p) { /* 将 params 转为组件 JSON 对象 */ },
  toCmd(p)  { /* 将 params 转为命令格式字符串 */ },
}
```

### 支持参数类型

| `param.type` | 说明 | 渲染组件 |
|-------------|------|---------|
| `text` | 单行文本 | `<input type="text">` |
| `number` | 数字 | `<input type="number">` |
| `richtext` | 富文本（Minecraft JSON 文本组件） | 弹出模态编辑器 |
| `checkbox` | 布尔开关 | `<input type="checkbox">` |
| `select` | 下拉选择 | `<select>` + 选项列表 |
| `kvlist_ench` | 键值列表（附魔格式） | 动态增删行 |
| `list_attr` | 属性修饰符列表 | 动态增删行 |
| `list_toolrule` | 工具规则列表 | 动态增删行 |
| `list_item` | 物品列表 | 动态增删行 |
| `list_banner` | 旗帜图案列表 | 动态增删行 |
| `list_potion` | 药水效果列表 | 动态增删行 |
| `json` | 原始 JSON | `<textarea>` |
| `textlist` | 文本列表 | 动态增删行 |
| `color_hex` | 十六进制颜色 | `<input type="text">` (#RRGGBB) |

---

## 输出示例

### `/give` 命令

```
/give @p minecraft:diamond_sword[minecraft:enchantments={levels:{"minecraft:sharpness":5,"minecraft:unbreaking":3}},minecraft:attribute_modifiers=[{type:"minecraft:generic.attack_damage",name:"weapon_damage",amount:10,operation:"add_value",slot:"mainhand"}],minecraft:rarity:"epic",minecraft:unbreakable:{}] 1
```

### 组件 JSON

```json
{
  "minecraft:enchantments": {
    "levels": {
      "minecraft:sharpness": 5,
      "minecraft:unbreaking": 3
    }
  },
  "minecraft:attribute_modifiers": [
    {
      "type": "minecraft:generic.attack_damage",
      "name": "weapon_damage",
      "amount": 10,
      "operation": "add_value",
      "slot": "mainhand"
    }
  ],
  "minecraft:rarity": "epic",
  "minecraft:unbreakable": {}
}
```

---

## 开发说明

- **浏览器兼容** — 目标为现代 Chromium 内核浏览器（Chrome / Edge 最新版）
- **编码规范** — ES6+ 无转译，使用 `const/let`、箭头函数、模板字符串、解构赋值
- **状态管理** — 当前为全量渲染模式（`renderPalette()` / `renderWorkspace()` 每次重绘全部 DOM），小规模场景下够用
- **数据流** — 单向数据流：用户操作 → `workspaceBlocks` 状态变更 → `renderWorkspace()` → `generateOutput()`

---

## License

本项目为个人作品，与 Mojang Studios / Microsoft 无关联。

Minecraft 是 Mojang Synergies AB 的商标。
