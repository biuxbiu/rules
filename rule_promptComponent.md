---
description: 将 React + Framer Motion 组件快速转换为详细的 AI Prompt，支持关键词触发，并自动保存为 .md 文件
alwaysApply: false
enabled: true
updatedAt: 2026-02-11T03:13:37.824Z
provider:
---

# Component to Prompt Converter

## 目的

快速将 React + Framer Motion 组件转换为详细的 AI Prompt 文档，方便他人通过 Prompt 重现相同效果。

## 触发方式

当用户提到以下任一关键词时自动应用此规则：

- `@prompt`
- `@convert`
- `转换成 prompt`
- `生成 prompt`
- `转成 prompt`

## 转换内容

### 必须包含的部分

#### 1. 功能需求

- 组件名称
- Props 定义（类型、可选性、作用）

#### 2. 布局要求

- 容器尺寸（固定/响应式）
- 布局方式（Grid/Flex）
- 间距、内边距
- 子元素数量、样式和长宽大小

#### 3. 动画要求

**父容器动画配置**：

- `variants` 定义（hidden/visible 状态）
- `transition` 配置：
  - `staggerChildren`（交错延迟）
  - `delayChildren`（整体延迟）
  - `when`（时序控制：beforeChildren/afterChildren）
  - `staggerDirection`（交错方向：1 正向/-1 反向）
- 父元素自身动画（如背景色、尺寸等）

**子元素动画配置**：

- hidden 状态的属性值
- visible 状态的属性值
- 动画类型（spring/tween）
- 弹簧参数（stiffness/damping/mass）
- 其他过渡参数

#### 4. 关键技术点

- 特殊配置的解释
- 动画时序逻辑
- 状态继承机制
- 需要注意的细节

#### 5. 预期效果

- 显示动画的执行流程
- 隐藏动画的执行流程
- 动画时序图（可选）

#### 6. 简化版 Prompt

- 一段式描述，包含核心配置
- 适合快速使用和复制

### 输出格式

#### 详细版（默认）

```markdown
## Prompt: [组件功能描述]

### 功能需求

...

### 布局要求

...

### 动画要求

...

### 关键技术点

...

### 预期效果

...

### 动画时序图（可选）

...

### 技术栈

- React + TypeScript
- Framer Motion
- Tailwind CSS
```

#### 简化版

```
使用 React 和 Framer Motion 创建 [功能描述]：

布局：
- [布局信息]

动画特性：
- [关键动画配置]

效果：
- [预期效果]

通过 [props] 控制，使用 variants 定义状态
```

## 适用文件类型

- `*.tsx` 组件文件
- 包含 `framer-motion` 导入
- 包含 `motion.div` 或其他 motion 组件

## 使用示例

### 简单触发

```
用户：@StaggerChildren.tsx @prompt
AI：自动分析组件并生成详细 + 简化版 Prompt
```

### 指定输出

```
用户：@StaggerChildren.tsx @prompt --simple
AI：仅输出简化版 Prompt
```

## 自动保存行为（重要）⭐ 省 Token 模式

**静默生成模式 - 不要输出详细内容到对话中！**

1. **立即创建 `.md` 文件**：
   - 文件名：与组件同名，如 `ComponentName.md`
   - 位置：与组件文件相同的目录
   - 内容：完整的详细版 Prompt

2. **文件创建步骤**：

   ```
   步骤1: 内部生成 Prompt 内容（不输出到对话）
   步骤2: 直接使用 write_to_file 工具创建 .md 文件
   步骤3: 仅输出简短确认信息
   ```

3. **输出格式（仅输出以下简短信息）**：

   ```
   ✅ 已生成 Prompt 文档: ComponentName.md

   核心特性: [一句话总结，不超过30字]
   ```

4. **禁止行为**：
   - ❌ 不要在对话中输出完整的 Prompt 内容
   - ❌ 不要展示详细的功能需求、布局要求等章节
   - ❌ 不要输出 Markdown 格式的长文档
   - ✅ 只输出简短的确认信息（2-3 行）

## 注意事项

1. 准确提取所有动画参数，不遗漏关键配置
2. 解释高级特性（when、staggerDirection 等）的作用
3. 提供清晰的时序说明，帮助理解动画执行顺序
4. 简化版要包含所有核心信息，但表述简洁
5. **必须自动创建 `.md` 文件**，无需询问用户

## 特殊处理

- 如果组件包含多个 motion 元素层级，分层描述
- 如果使用了自定义 transition 函数，详细说明
- 如果有条件动画，说明触发条件
- 如果 `.md` 文件已存在，覆盖旧内容
