# 版本历史

这里记录 Pinyin IME 的正式发布版本、下载地址和完整性校验信息。

| 版本 | 发布日期 | 最低 KOReader | 下载 | SHA-256 |
| --- | --- | --- | --- | --- |
| [v1.1.0](v1.1.0.md) | 2026-07-27 | v2025.10 | [ZIP](https://github.com/Merpyzf/pinyinime.koplugin/releases/download/v1.1.0/pinyinime.koplugin-v1.1.0.zip) | `f5319ae0253dbab2f6e7f94ab204b3de8ca69634451294e33a3d037572ddee36` |
| [v1.0.0](v1.0.0.md) | 2026-07-18 | v2025.10 | [ZIP](https://github.com/Merpyzf/pinyinime.koplugin/releases/download/v1.0.0/pinyinime.koplugin-v1.0.0.zip) | `c4e2a46eff38952a84f752b5bae09a9e775af0cf9e55a5c9bc5fbc5df25098da` |

当前最新版为 **v1.1.0**。机器可读的最新版信息见 [index.json](index.json)。

## 校验下载文件

macOS 或 Linux：

```sh
shasum -a 256 pinyinime.koplugin-v1.1.0.zip
```

Windows PowerShell：

```powershell
Get-FileHash .\pinyinime.koplugin-v1.1.0.zip -Algorithm SHA256
```

计算结果应与本页、对应版本记录以及 Release 资产中的 `SHA256SUMS.txt` 完全一致。
