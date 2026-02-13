# PROJECT KNOWLEDGE BASE

**Generated:** 2026-02-13 (updated)
**Structure:** Single-file SPA

## OVERVIEW

CodeGlyph (码上生花) - 中文字符编码练习工具，基于间隔重复算法。单文件架构，无构建流程。

## STRUCTURE

```
code-glyph/
├── index.html    # 完整应用 (HTML+CSS+JS, ~720行)
└── GEMINI.md     # 项目文档 (详细功能说明)
```

## WHERE TO LOOK

| 任务 | 位置 | 备注 |
|------|------|------|
| UI样式 | `index.html:7-176` | CSS变量在 `:root` |
| DOM缓存 | `index.html:226-248` | 全局 `DOM` 对象 |
| SRS核心算法 | `index.html:269-377` | `getNextChar`, `handleInputComplete` |
| 码表解析 | `index.html:621` | `parseAndMergeDict` (YAML格式) |
| 本地存储 | `index.html:417-447` | `codeGlyphProfiles` 键 |
| 预置文本 | `index.html:250-258` | `PREDEFINED_TEXTS` 常用字 |
| 预置码表 | `index.html:258` | `PREDEFINED_DICTS` 远程URL |

## CODE MAP

| 函数 | 行号 | 职责 |
|------|------|------|
| `getCharStat` | 270 | 获取/初始化字符统计 |
| `getNextChar` | 281 | SRS调度：选择下一字符 |
| `handleInputComplete` | 315 | 正确/错误处理，更新间隔 |
| `startPracticeSession` | 496 | 初始化练习会话 |
| `nextCharacter` | 522 | 显示下一字符 |
| `parseAndMergeDict` | 621 | 解析Rime YAML码表 |
| `exportProgress` | 647 | 导出JSON进度 |
| `importProgress` | 674 | 导入进度文件 |

## CONVENTIONS

- **单文件架构**: 所有代码在 `index.html`，不拆分
- **全局DOM**: 用 `DOM.xxx` 访问元素，避免重复查询
- **状态变量**: `dictionary`, `practiceSet`, `currentProfile`, `currentCharacter`
- **localStorage**: `codeGlyphProfiles` 存所有进度，按码表ID分profile

## ANTI-PATTERNS

- **禁止**: 拆分成多文件（保持单文件架构）
- **禁止**: 引入构建工具或依赖
- **禁止**: 修改 `parseAndMergeDict` 格式（需兼容Rime YAML）
- **注意**: `index.html:724-727` 有重复闭合标签 `</body></html>`（应删除726-727行）
- **注意**: `index.html:234` 有重复定义 `uploadDictBtn`（与233行重复）

## UNIQUE STYLES

- 中文UI，变量名用英文
- CSS变量主题化: `--primary-color`, `--danger-color`
- 反馈动画: `.shake` keyframes

## COMMANDS

```bash
# 运行: 直接浏览器打开
open index.html

# 无构建、无测试、无依赖
```

## NOTES

- 远程码表来自 `raw.githubusercontent.com/sbsrf/sbsrf`
- 旧版profile格式会自动迁移 (`migrateOldProfile`)
- `sessionMistakeQueue` 用于会话内错误字符优先复习
