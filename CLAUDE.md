# CLAUDE.md

# 116 學年度專題及創意製作競賽：影音評分系統

由 115 學年度系統（`fbkstj/cr6`）複製而來，程式與流程相同，資料全部重來。**開新對話先讀 `進度紀錄.md`**；設計依據是 `開發計畫書.md`，部署步驟見 `部署說明.md`，後台操作見 `後台操作步驟.md`。

- 磁碟代號每台電腦不同，不要寫死在腳本或文件裡。
- 在 Bash 工具執行 Python 時設 `PYTHONIOENCODING=utf-8`。
- 學生影片、帳號密碼、API 金鑰、GitHub token 不可放進公開 repo 或寫進檔案；密碼一律由老師自己輸入。
- 本資料夾是公開 repo `fbkstj/116` 的本機副本，網站 https://fbkstj.github.io/116/ （Pages 從根目錄發布）。推送等於公開發布，先問老師。
- **Supabase 要用 116 專用的新專案**（待建立，代碼記在進度紀錄）。**不要對 115 的 `ciovykuhvpelghrjlutp`、也絕對不要對重補修的 `mcewgfzeqhdpygfvbfij` 下任何指令**；兩者網頁上同名，一律用代碼辨認。
- 學校網路擋資料庫連接埠 5432／6543：改用 `npx.cmd supabase db query --remote=<代碼> --yes --file <sql>`（走 HTTPS），套用後登記到 `supabase_migrations.schema_migrations`；`functions deploy` 不受影響。CLI 變更要加 `--yes`，部署前先問老師。

## 開發與測試

- `node test/run.mjs`、`node test/check_sql.mjs`（需 `PGLITE_DIR`，見檔頭）、`python test/test_videos.py`；改程式後三個都要跑。
- 本機開發：`python test/make_demo_videos.py` → `node test/devserver.mjs`，http://localhost:8790/ ，測試帳號 admin01／admin-pass-01、judge01～05／judge-pass-01～05（合成資料）。
- 資料庫關鍵寫入都在 SQL 函式（`supabase/migrations/`），`test/memdb.mjs` 用 JS 照同樣規則實作；改規則時兩邊都要改。
