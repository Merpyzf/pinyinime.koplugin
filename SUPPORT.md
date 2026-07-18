# 支持与故障反馈

本页帮助你在提交问题前收集必要信息，同时避免泄露个人输入数据。

## 先做这几项检查

1. 确认插件目录为 `koreader/plugins/pinyinime.koplugin/`，并且其中直接包含 `main.lua`。
2. 重启 KOReader，确认简体中文键盘已启用。
3. 进入 `设置 → 设备 → 键盘 → 拼音输入法`，核对插件版本。
4. 打开“运行状态与诊断”，记录运行状态、兼容性验证和实际词库模式。
5. 如果完整词库回退，请确认 `data/wanxiang.sqlite3` 与 `data/academic_supplement.sqlite3` 都已复制完整。

## 提交问题时请提供

- 设备品牌与具体型号；
- KOReader 版本；
- Pinyin IME 版本；
- 问题出现在哪一种输入框；
- 使用的输入方案；
- 可重复的操作步骤；
- 预期结果与实际结果；
- “运行状态与诊断”的文字或截图；
- 如有异常提示，可附上其中的“技术详情”。

建议先用不会涉及个人内容的测试文本重现问题，例如 `nihaoshijie` 或 `zhongwen`。

## 请不要上传

- `koreader/settings/chinesepinyin.lua`；
- 包含私人书名、搜索记录、笔记或账号信息的截图；
- 整个 KOReader 设置目录；
- 未经删减的设备备份。

`chinesepinyin.lua` 可能包含候选偏好和个人词语关联。多数问题只需要诊断页面、版本信息和复现步骤即可定位。

## 反馈渠道

请在 [GitHub Issues](https://github.com/Merpyzf/pinyinime.koplugin/issues) 提交问题。标题建议使用“设备型号 + 简短现象”，例如：

```text
Kindle Paperwhite 5：完整词库启动后回退到兼容词库
```

## 安全恢复

如果插件影响当前输入，可先在 KOReader 插件管理器中停用它并重启。也可以在退出 KOReader 后移除 `koreader/plugins/pinyinime.koplugin/`；KOReader 会恢复原有简体中文输入行为。
