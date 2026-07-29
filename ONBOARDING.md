# ONBOARDING — 讓你的 AI 接上這個知識庫

> 原則：**你的 rule 檔只放入口指標,契約住在庫內 `AGENTS.md`**。rule 檔是你自己維護的分散副本,寫入細節必然過期;契約隨每次發布更新,改一次全員生效。

## 形式①:clone + rule 指標(預設,適合 Claude Code / Cursor / Codex CLI 等有檔案工具的 agent)

1. clone 本 repo(需 read 權限):

```bash
git clone https://github.com/erikhuang76821/novel-dist.git
```

2. 在你自己的 rule 檔(CLAUDE.md / .cursorrules / GEMINI.md / AGENTS.md)加**三行**:

```
《無極封》知識庫在 <你的路徑>/novel-dist(唯讀)。
查庫前先在該目錄 git pull 取最新版。
進庫先讀它的 AGENTS.md,照其中契約檢索與引用。
```

就這樣。**不要**把庫內結構或知識內容抄進 rule 檔(會過期);**不要**指向庫內深層路徑(結構由 CI 演進)。

## 形式②:GitHub MCP(免 clone,適合 Claude Desktop 等)

在你的 client 接 GitHub 官方 MCP connector(用你的 GitHub 身分),即可遠端讀取本 repo。注意:每讀一檔是一次 API 呼叫,且 GitHub 搜尋對中文斷詞差 —— **更要照 AGENTS.md 走 `_derived/` 索引層**,不要全文搜尋。

## 形式③:git submodule(需要鎖定知識庫版本的專案)

```bash
git submodule add https://github.com/erikhuang76821/novel-dist.git kb/novel
```

commit-pinned、可重現;升版手動 `git submodule update --remote`。非預設,只在你需要「重現某個 release 當下的答案」時用。

## 反模式(請勿)

- ❌ 把知識內容貼進 rule / system prompt —— context 膨脹 + 立即過期
- ❌ rule 指向庫內深層路徑(如 `_derived/index-001.json`)—— 分片邊界會變
- ❌ 拿 commit 日期推斷劇情進度 —— 以 `_derived/manifest.json` 的 `coverage` 為準

## 回饋

發現內容錯誤 → 開本 repo 的 Issue(有「知識庫內容錯誤回報」模板;附上 manifest 的 `release_id`、檔案路徑、原文片段)。
