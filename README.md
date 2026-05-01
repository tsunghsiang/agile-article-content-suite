# agile-article-content-suite

A bundled Claude skill suite for end-to-end agile content creation on Medium.

## Workflow

```
[1] agile-topic-scout          → 發掘 10 個熱門 agile 主題
        ↓ 點選主題
[2] agile-article-writer       → 產出文章大綱 + Medium SEO 套件
        ↓ /agile-post-writer
[3] agile-post-writer          → 以 @uragilecoach 語氣撰寫完整 Medium 文章
        ↓ /agile-illustration-generator
[4] agile-illustration-generator → 產出封面圖 + 文中插圖（SVG/HTML）
```

## 檔案結構

```
agile-article-content-suite/
├── SKILL.md                          # 主入口：工作流程說明 + 路由邏輯
├── README.md                         # 本文件
└── skills/
    ├── agile-topic-scout.md          # Stage 1：主題探索
    ├── agile-article-writer.md       # Stage 2：文章大綱 + SEO
    ├── agile-post-writer.md          # Stage 3：完整 Medium 文章
    └── agile-illustration-generator.md  # Stage 4：視覺插圖
```

## 安裝方式

### 方法一：下載 `.skill` 檔安裝

1. 到 [Releases](../../releases) 下載最新的 `agile-article-content-suite.skill`
2. 在 Claude.ai 的 Skills 介面點右上角 **+**
3. 選擇「Upload skill file」匯入

### 方法二：用 skill-creator 打包

```bash
git clone https://github.com/your-username/agile-article-content-suite
cd agile-article-content-suite
python -m scripts.package_skill . --output agile-article-content-suite.skill
```

## 修改 Sub-Skills

每個 sub-skill 都是獨立的 Markdown 檔案，直接編輯 `skills/` 底下對應的 `.md` 即可。
修改後重新打包上傳到 Releases，或直接請 Claude 從 repo 拉取修改。

## 觸發方式

| 指令 | 效果 |
|------|------|
| `agile content workflow` | 啟動整個 suite，從頭開始 |
| `/agile-topic-scout` | 直接進入主題探索 |
| `/agile-article-writer` | 直接進入文章大綱 |
| `/agile-post-writer` | 直接進入 Medium 文章撰寫 |
| `/agile-illustration-generator` | 直接進入插圖生成 |
