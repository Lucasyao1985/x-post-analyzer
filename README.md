# X/Twitter 帖子分析器 (x-post-analyzer)

自动获取并分析 X（Twitter）帖子内容，输出结构化中文分析报告。

## 功能特性

- 解析 X/Twitter 帖子链接（x.com / twitter.com）
- 获取帖子内容：正文、媒体、引用、互动数据、回复
- 输出结构化中文分析报告
- 支持单 Agent 顺序回退，多数据源容错

## 安装

```bash
git clone https://github.com/Lucasyao1985/x-post-analyzer.git
```

## 使用示例

```
帮我分析这个推文：https://x.com/user/status/123

这个 X 帖子说了什么？

分析这条推文的内容
```

## Skill 文件结构

```
x-post-analyzer/
├── SKILL.md           # 主技能文件
├── README.md          # 项目说明
├── scripts/           # 执行脚本
├── references/        # 参考资料
└── assets/            # 资源文件
```

## License

MIT
