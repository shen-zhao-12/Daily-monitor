# 线口监测 · 云端版(网页上传专用版)

每天北京时间 **09:00 / 15:00** 在 GitHub 云端自动运行:抓取各线口信源 → 通义千问总结分级 → 生成 Word 简报和网页。电脑关机不影响。

六大线口:AI/大模型 · 机器人/AI硬件 · 无人驾驶/低空/智慧出行 · 电商/直播/即时零售 · 游戏/电竞/平台公司 · 消费/以旧换新/新餐饮

> 本包专为"网页上传"方式准备:GitHub 上传页不接受 `.github` 隐藏文件夹,所以工作流文件改为网页编辑器手动创建(见第3步,只需复制粘贴一次)。

## 部署步骤(约10分钟)

### 第1步:创建 GitHub 仓库
1. 打开 https://github.com/new
2. Repository name 填 `beat-monitor`(或任意英文名),选 **Public**,点 Create repository

### 第2步:上传文件
1. 进入新仓库页面,点 **Add file → Upload files**
2. 把本文件夹里的这些拖进去:**monitor.py、requirements.txt、README.md、web 文件夹**
   (「工作流内容…….txt」这个文件**不要**上传,它是第3步复制用的)
3. 点 Commit changes

### 第3步:创建定时任务文件(关键步骤)
1. 回到仓库页面,点 **Add file → Create new file**
2. 在文件名输入框里输入:`.github/workflows/monitor.yml`
   (输完 `.github/` 会自动变成文件夹,继续输完整个路径)
3. 双击打开本文件夹里的「工作流内容(这个文件不要上传,打开复制用).txt」,**Cmd+A 全选 → Cmd+C 复制**
4. 回到 GitHub 的大编辑框,**Cmd+V 粘贴**
5. 点右上角 **Commit changes**

### 第4步:开通网页托管
1. 仓库页面点 **Settings → Pages**
2. Source 选择 **GitHub Actions**(不要选 Deploy from a branch)

### 第5步:配置通义 API Key
1. 打开 https://bailian.console.aliyun.com (阿里云百炼,用支付宝/淘宝账号即可登录)
2. 左侧「API-KEY」→ 创建 API Key,复制(新用户有免费额度)
3. 回到 GitHub 仓库:**Settings → Secrets and variables → Actions → New repository secret**
4. Name 填 `DASHSCOPE_API_KEY`,Value 粘贴 Key,点 Add secret

### 第6步:手动跑一次验证
1. 仓库页面点 **Actions** 标签 → 左侧选「线口监测」→ 右侧 **Run workflow** 按钮
2. 等 2-3 分钟变绿勾,打开 `https://你的用户名.github.io/beat-monitor/` 查看网页
3. 之后每天 09:00、15:00 自动运行,无需任何操作

## 日常维护

- **改监测领域/关键词**:编辑 `monitor.py` 顶部的 `QUERIES`、`ENTITY_QUERIES`、`BEATS`(网页上直接点文件→铅笔图标编辑→Commit 即可)
- **额度用完**:脚本自动降级为无摘要模式,网页照常更新;充值或更换 Key 后在 Secrets 里更新即可
- **手动加跑**:Actions → 线口监测 → Run workflow
- **网页数据**:最近 60 期简报存档,每期可下载 Word

## 说明

- GitHub 定时任务可能有 10-30 分钟延迟,属正常现象
- 抓取窗口为近 48 小时,去重后由通义筛选分级(A=值得立即跟进 / B=选题储备 / C=背景参考)
- 涉及广州/广东/大湾区的线索自动标注「本地」
- 如果第6步 Actions 里看不到「线口监测」,说明第3步的文件路径没建对,检查是否正好是 `.github/workflows/monitor.yml`
