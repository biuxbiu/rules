---
description: Icon 组件开发规范 - 标准 Icon 组件创建指南
alwaysApply: false
enabled: true
updatedAt: 2026-02-26T02:29:47.104Z
provider:
---

# Icon Component Development Rule

## 目的

规范 Icon 组件的创建标准，提供统一的开发模板和最佳实践。

## 参考资源

1. **优先参考项目中的现有组件**：
   - 查看 `src/components/Icon.tsx` 中的现有 Icon 组件
   - 参考现有 Icon 的设计风格、命名方式和实现细节
   - 保持项目内 Icon 的一致性

2. **当没有思路时参考以下图标资源**：
   - **Google Fonts Icons**: https://fonts.google.com/icons
     - 提供大量免费的 Material Design 图标
     - 可直接复制 SVG 代码进行修改
     - 参考其设计风格和命名方式
   - **Icons8**: https://icons8.com/icons
     - 提供丰富的图标库和多种风格
     - 支持自定义颜色、大小和格式
     - 可下载 SVG 格式进行修改
   - **Flaticon**: https://www.flaticon.com
     - 海量免费图标资源库
     - 多种设计风格可选
     - 支持 SVG、PNG 等多种格式下载
   - **Lucide Icons**: https://lucide.dev/icons
     - 简洁现代的开源图标库
     - 与项目风格高度契合（strokeWidth="2", round 风格）
     - 提供 React 组件参考

## 触发方式

当用户提到以下关键词时应用此规则：

- `@icon`
- `创建 icon`
- `新增 icon`
- `icon 组件`
- `画 icon`
- `设计 icon`

---

## 标准 Icon 组件规范

### 1. Props 类型定义（必须）

```typescript
type IconProps = {
  size?: number; // 图标尺寸，默认 24
  color?: string; // 图标颜色，默认 currentColor
  className?: string; // 额外的 CSS 类名
};
```

### 2. 完整组件模板

```typescript
export const IconRight: React.FC<IconProps> = ({
  size = 24,
  color = "currentColor",
  className,
}) => {
  return (
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width={size}
      height={size}
      viewBox="0 0 24 24"
      fill="none"
      stroke={color}
      strokeWidth="2"
      strokeLinecap="round"
      strokeLinejoin="round"
      className={className}
    >
      <g>
        <path d="M5 12h14"></path>
        <path d="m12 5 7 7-7 7"></path>
      </g>
    </svg>
  );
};
```

### 3. 属性映射规则（关键）

| Props 属性  | SVG 属性            | 说明                                             |
| ----------- | ------------------- | ------------------------------------------------ |
| `size`      | `width` 和 `height` | 同时设置宽高，保持原始比例                       |
| `color`     | `stroke` ｜ `fill`  | 使用 `currentColor` 继承父元素颜色               |
| `className` | `className`         | 直接传递，支持 Tailwind 等样式                   |
| -           | `xmlns`             | **固定为 "http://www.w3.org/2000/svg"**          |
| -           | `strokeWidth`       | **固定为 "2"**（与 Icon.tsx 保持一致的标准线宽） |
| -           | `strokeLinecap`     | **固定为 "round"**（圆角端点，保持圆润效果）     |
| -           | `strokeLinejoin`    | **固定为 "round"**（圆角连接，保持圆润效果）     |

### 4. 命名规范

#### 组件命名

```typescript
// ✅ 正确命名
export const IconRight; // 方向：右
export const IconArrowUp; // 箭头：上
export const IconCheckCircle; // 状态：勾选圆圈
export const IconAlertTriangle; // 警告：三角形
export const IconImage; // 图片：加载失败

// ❌ 错误命名
export const RightIcon; // 后缀错误
export const icon_right; // 下划线格式错误
export const Right; // 缺少 Icon 前缀
```

**命名规则**：

- 必须以 `Icon` 开头
- 使用 PascalCase（大驼峰）
- 名称要具有描述性
- 多个单词直接连接，无下划线或连字符

#### 文件存放位置

```
src/components/
├── Icon.tsx           # 通用图标（主要文件）
├── IconAd.tsx         # 广告相关图标
└── IconLibrary.tsx    # 图标库专用图标
```

### 5. 创建新 Icon 的步骤清单

- [ ] 1. 复制标准模板代码
- [ ] 2. 修改组件名称（遵循命名规范）
- [ ] 3. 确保 Props 类型为 `IconProps`
- [ ] 4. 设置默认值：`size = 24`, `color = "currentColor"`
- [ ] 5. 将所有 SVG 属性映射正确：
  - [ ] `xmlns="http://www.w3.org/2000/svg"`
  - [ ] `width={size}`
  - [ ] `height={size}`
  - [ ] `stroke={color}`
  - [ ] `strokeWidth="2"`
  - [ ] `strokeLinecap="round"`
  - [ ] `strokeLinejoin="round"`
  - [ ] `className={className}`
- [ ] 7. 测试不同 size 和 color 的显示效果
- [ ] 8. 确认在不同背景下的可见性

### 6. 常见错误及修复

#### 错误 2: 使用错误的属性名

```typescript
// ❌ 错误（React 中必须使用驼峰命名）
<svg stroke-width="2" stroke-linecap="round" stroke-linejoin="round">

// ✅ 正确
<svg strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
```

#### 错误 3: 硬编码尺寸和颜色

```typescript
// ❌ 错误
<svg width="24" height="24" stroke="#000000">

// ✅ 正确
<svg width={size} height={size} stroke={color}>
```

#### 错误 4: 缺少 className 支持

```typescript
// ❌ 错误
export const IconExample: React.FC<IconProps> = ({ size = 24, color = "currentColor" }) => {
  return <svg>...</svg>;
};

// ✅ 正确
export const IconExample: React.FC<IconProps> = ({ size = 24, color = "currentColor", className }) => {
  return <svg className={className}>...</svg>;
};
```

### 7. 使用示例

#### 基础使用

```tsx
<IconRight />
```

#### 自定义尺寸

```tsx
<IconRight size={32} />
<IconRight size={16} />
```

#### 自定义颜色

```tsx
<IconRight color="#ff0000" />
<IconRight color="blue" />
<IconRight /> {/* 继承父元素的 color */}
```

#### 添加样式

```tsx
<IconRight className="hover:text-blue-500 transition-colors" />
```

#### 组合使用

```tsx
<button className="flex items-center gap-2">
  <IconRight size={20} />
  <span>Next</span>
</button>
```

---

## 技术栈

- React 18+ with TypeScript
- SVG 1.1
- Tailwind CSS（可选）

## 设计原则

1. **一致性**: 所有 Icon 使用相同的 Props 接口
2. **灵活性**: 通过 Props 控制尺寸、颜色和样式
3. **可访问性**: 支持 className 传递，方便添加 aria 属性
4. **性能**: 纯 SVG 实现，无外部依赖
5. **可维护性**: 标准化模板，易于创建和修改

## 测试清单

- [ ] Icon 在不同尺寸下正确显示（16px, 24px, 32px, 48px）
- [ ] Icon 在不同颜色下正确显示
- [ ] Icon 在浅色和深色背景下都可见
- [ ] className prop 正常工作
- [ ] TypeScript 类型检查通过
- [ ] 无控制台错误或警告

## 使用场景示例

### 创建新 Icon

```bash
用户: @icon 帮我创建一个搜索图标
AI:
1. 首先查看 src/components/Icon.tsx 中是否有类似的现有组件
2. 参考现有组件的设计风格创建新组件
3. 如果没有合适的参考，可查看 Google Fonts Icons (https://fonts.google.com/icons)
4. 根据标准模板创建 IconSearch 组件
```

```bash
用户: @icon "svg 内容"
AI: 根据标准模板创建一个 Icon 组件
```

```bash
用户: @icon "svg 内容" [名字]
AI: 根据标准模板创建一个 Icon 组件，并且根据提供的名字来命名
```

### 修复 Icon 问题

```bash
用户: @icon 为什么我的图标尺寸不对？
AI: 检查是否正确映射了 width={size}
```

## 注意事项

1. **标准化优先**: 所有 Icon 必须遵循统一的 Props 和 SVG 属性映射
2. **命名一致**: 严格遵循 `Icon{Name}` 的命名规范
3. **默认值**: 始终设置 `size = 24`, `color = "currentColor"`
4. **固定属性**: strokeWidth、strokeLinecap、strokeLinejoin 保持固定值
5. **测试完整**: 确保在不同场景下都能正确显示
6. **代码复用**: 使用标准模板，避免重复定义 Props 类型
7. **任务执行状态**: 执行完任务之后，只返回任务结果，不展示任务组件代码。
