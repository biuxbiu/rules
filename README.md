# Development Rules Collection

一套用于提升开发效率的自动化规则集合,包含 Git 自动提交、Icon 组件标准化和组件文档转换等工具。

## 📦 规则列表

### 1. Git 自动提交规则 (`rule_git.md`)

自动化 Git 提交流程,根据代码改动内容智能生成符合规范的 commit message。

**核心功能:**
- 🤖 智能分析代码改动类型
- ✨ 自动生成带 Emoji 的 commit message
- 🚀 一键完成 add + commit + push 流程
- 🔒 提交前安全检查(敏感信息、语法错误等)

**触发关键词:**
- `@gt`
- `提交代码`
- `git 提交`
- `commit`
- `push 代码`

**Commit Message 格式:**
```
<emoji> <简短描述>
```

支持的类型包括:
- ✨ 新功能
- 🐛 Bug修复
- 📝 文档更新
- 🎨 样式优化
- ♻️ 代码重构
- ⚡️ 性能优化
- 🔧 配置修改
- 等等...

---

### 2. Icon 组件开发规范 (`rule_IconComponent.md`)

标准化 Icon 组件的创建流程,提供统一的开发模板和最佳实践。

**核心功能:**
- 📐 统一的组件接口规范(`IconProps`)
- 🎨 标准化 SVG 属性映射
- 🔄 支持自定义尺寸、颜色和样式
- 📚 提供多个图标资源参考链接

**触发关键词:**
- `@icon`
- `创建 icon`
- `icon 组件`

**标准组件模板:**
```typescript
type IconProps = {
  size?: number;        // 默认 24
  color?: string;       // 默认 currentColor
  className?: string;
};

export const IconExample: React.FC<IconProps> = ({
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
      {/* SVG 路径 */}
    </svg>
  );
};
```

**参考资源:**
- [Google Fonts Icons](https://fonts.google.com/icons)
- [Lucide Icons](https://lucide.dev/icons)
- [Icons8](https://icons8.com/icons)
- [Flaticon](https://www.flaticon.com)

---

### 3. 组件转 Prompt 工具 (`rule_promptComponent.md`)

快速将 React + Framer Motion 组件转换为详细的 AI Prompt 文档。

**核心功能:**
- 📄 自动提取组件功能、布局和动画配置
- 💾 自动保存为 `.md` 文件
- 🎯 生成详细版和简化版两种格式
- ⚡️ 节省 Token,采用静默生成模式

**触发关键词:**
- `@prompt`
- `@convert`
- `转换成 prompt`
- `生成 prompt`

**输出内容包括:**
- 功能需求分析
- 布局要求说明
- 动画配置详情
- 关键技术点解释
- 预期效果描述
- 简化版 Prompt

**使用示例:**
```
用户: @ComponentName.tsx @prompt
AI: ✅ 已生成 Prompt 文档: ComponentName.md
```

---

## 🚀 使用场景

### Git 提交场景
```bash
# 场景1: 快速提交
用户: @gt
AI: 自动分析改动 → 生成 commit message → 执行提交

# 场景2: 添加新功能后提交
修改多个文件后...
用户: 提交代码
AI: ✨ 添加用户资料组件
```

### Icon 创建场景
```bash
# 场景1: 从零创建
用户: @icon 帮我创建一个搜索图标
AI: 根据标准模板创建 IconSearch 组件

# 场景2: 从 SVG 创建
用户: @icon <svg>...</svg> Search
AI: 转换为标准 IconSearch 组件
```

### 组件转换场景
```bash
# 场景1: 转换为文档
用户: @StaggerChildren.tsx @prompt
AI: ✅ 已生成 Prompt 文档: StaggerChildren.md

# 场景2: 仅需简化版
用户: @StaggerChildren.tsx @prompt --simple
AI: 输出简化版 Prompt
```

---

## 🛠 技术栈

- React 18+ with TypeScript
- Framer Motion
- Tailwind CSS
- Git
- SVG 1.1

---

## 📋 最佳实践

### Git 提交
1. **原子提交**: 每次提交只做一件事
2. **及时提交**: 完成小功能就提交
3. **清晰描述**: 让他人能快速理解改动
4. **避免大规模提交**: 拆分成多次提交

### Icon 组件
1. **一致性**: 使用统一的 Props 接口
2. **命名规范**: 严格遵循 `Icon{Name}` 格式
3. **默认值**: 始终设置标准默认值
4. **测试完整**: 确保各种场景下正确显示

### Prompt 转换
1. **准确提取**: 不遗漏关键配置
2. **清晰说明**: 提供时序和逻辑解释
3. **自动保存**: 直接生成 `.md` 文件
4. **节省 Token**: 采用静默生成模式

---

## 📖 规则文件说明

| 文件名                     | 说明                          | 类型       |
| -------------------------- | ----------------------------- | ---------- |
| `rule_git.md`              | Git 自动提交规则              | 自动化工具 |
| `rule_IconComponent.md`    | Icon 组件开发规范             | 开发规范   |
| `rule_promptComponent.md`  | 组件转 Prompt 工具            | 转换工具   |

---

## 🎯 设计原则

1. **自动化优先**: 减少重复劳动,提升开发效率
2. **标准化**: 统一代码风格和提交规范
3. **灵活性**: 支持自定义配置和扩展
4. **可维护性**: 清晰的文档和示例
5. **实用性**: 解决实际开发中的痛点

---

## 📝 许可证

MIT License

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request!

---

**Made with ❤️ for better development experience**
