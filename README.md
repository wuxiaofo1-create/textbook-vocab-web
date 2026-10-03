# 主题单词卡片助手 · textbook-vocab-web

一个采用 Agent Skills 文件结构的技能包：取得教材或主题词汇，先让使用者审核词表及主题，再生成真实插画，并用固定模板制作可朗读、可选图、可翻页核对的电脑单词卡片。

## 给安装这个技能的 agent

- 技能名称：`textbook-vocab-web`。
- 仓库：`https://github.com/wuxiaofo1-create/textbook-vocab-web`。
- 默认分支：`main`。
- **技能位于仓库根目录，入口是 `SKILL.md`，不是仓库里的同名子目录。**
- 安装完整目录，保留 `references/` 与 `assets/`；只下载 `SKILL.md` 会缺少流程和模板。
- 将目录安装为 `textbook-vocab-web`，所有资源路径相对于技能根目录解析。
- 安装后先读取 `SKILL.md`，按其中链接读取相关资源；制作结果保存到用户输出目录。

可以直接把这段话发给支持技能安装的 agent：

```text
请从 https://github.com/wuxiaofo1-create/textbook-vocab-web 安装 Skill。
分支 main，技能路径为仓库根目录，安装名称 textbook-vocab-web。
请保留 SKILL.md、references/、assets/ 的完整结构，安装后读取 SKILL.md。
如果使用 Codex 的 skill-installer，参数为：
--repo wuxiaofo1-create/textbook-vocab-web --ref main --path . --name textbook-vocab-web
如果已有同名技能，请报告现状，不擅自覆盖我的本地修改。
```

`--path .` 表示仓库根目录；使用此参数时应同时指定 `--name textbook-vocab-web`。

## 手动安装

支持 Agent Skills 的客户端，可按该客户端的要求导入整个技能目录。下载 GitHub 的仓库 ZIP 后，根文件夹中应同时有 `SKILL.md`、`references/` 和 `assets/`；需要指定目录名称时改为 `textbook-vocab-web`。不要导入单独的 HTML 或单独的 `SKILL.md`。

Codex 用户在已有 Git 的电脑上，也可用以下命令安装到技能目录。已有同名目录时，先通过客户端更新或另行备份；命令不会替你覆盖。

macOS / Linux：

```bash
git clone https://github.com/wuxiaofo1-create/textbook-vocab-web.git "${CODEX_HOME:-$HOME/.codex}/skills/textbook-vocab-web"
```

Windows PowerShell：

```powershell
$vocabCodexRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE '.codex' }
git clone https://github.com/wuxiaofo1-create/textbook-vocab-web.git (Join-Path $vocabCodexRoot 'skills\textbook-vocab-web')
```

安装后开启新的对话／让客户端重新加载技能，在支持显式调用的 Codex 环境中使用 `$textbook-vocab-web`。

## 使用

例如：

```text
使用 $textbook-vocab-web，把我提供的这一课词表做成电脑单词卡片。
主题是小猪佩奇的学校生活。先展示词表、主题安排及预计素材图数，
等我确认后，再制作真实插画和网页。
```

也可以提供教材版本、年级、册次和课名，让 agent 先查来源；找不到匹配资料时再补照片或词表。未指定主题时技能会先询问，未确认词表时不会继续生成。

默认学习流程为：看英文、点击朗读 → 从四图中选择 → 翻页看正确图片及中文 → 下一个词。错图先按真实图义筛选，再随机抽取和排列；含义重叠、无法组成唯一正确答案的词保留翻页回想。图片按最多四词的四宫格素材制作，程序自动取图；不要求家长裁图或排版。

## 运行前提

- Agent 能读取技能资源并创建文件，才能生成单文件 HTML。
- 要查教材需联网／材料读取能力；已有词表或照片时可按提供的材料处理。
- 插画需要 agent 实际可用的生图工具，或使用者返回真实原图。技能本身不包含生图模型、API 密钥、登录授权或付费额度；没有生图能力时会先交付生图提示词并等待原图。
- 成品验证需要浏览器或客户端网页预览。朗读使用浏览器语音，声音和可用性取决于电脑及浏览器。

安装成功不等于以上外部能力都已具备。能力缺项时按技能流程说明，不以代码图形冒充真实插画，不把保存代码当作已经打开验证的网站。主要面向豆包电脑版的制作场景；其他支持 Agent Skills 的客户端按实际能力使用，不保证所有版本都提供相同入口或工具。

## 文件

```text
textbook-vocab-web/
├── SKILL.md
├── README.md
├── references/
│   ├── workflow.md
│   └── illustration.md
└── assets/
    └── vocab-pages.html
```

仓库只包含技能、所需文档和固定模板；没有本次测试词库、成品网页、图片、账号凭据或生成记录。
