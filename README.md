# hack-v1-tm14-di-yi-ci-bi-sai

# Drop Verse | Web3 Alpha 智能情报Agent

## 项目简介
Drop Verse 是一个构建于 Eliza OS 框架之上的 Web3 专属 AI Agent，专注于帮助用户（尤其是加密新手与散户）精准追踪：

- 代币生成事件（TGE）
- 公募项目（IDO、ICO、IEO）
- 空投机会或教程
- 一些币种的新闻

Drop Verse 不发布臆测、不制造噪音，仅转发来自可信来源的可验证信息。

理念：
- 帮助推广小型中文区Web3博主，让更多人看到他们的作品，不让顶部KOL控制
- 整合所有信息，让散户通过我们的Agent获取市场上所有可能在Web3赚钱的机会（不包含任何合约行为或金融建议）

## 团队信息
| 推特            | 信息                         | 工作内容（定位）                     |
|-----------------|-----------------------------|-----------------------------------|
| @lkzchain0415   | 北理， 计算机专业            | Twitter行为实现、处理后端逻辑、提问模板处理 |
| @potato89757_3  | 央财， 金融专业              | Agent角色设定、Knowledge处理   |
| @yunghwei       | 清华， 人工智能专业          | 数据爬取、提问模板处理     |
| @guoying2026    | 律动后端工程师（BlockBeats） | 处理TEE的部署，团队的老师  |

## 核心功能

**1. Alpha 信号捕捉**  
自动识别发币、公募、TGE 等关键事件信号，来源包括官方公告、头部媒体、Launchpad 发布等。

**2. 空投教程筛选**  
识别可信账号发布的高质量空投教程并转发，并保持中立的角度转载帖子，偶尔会警惕用户。

**3. 引用转推系统**  
自动引用或转发可信账号内容，并使用自身语气重新组织语言发布，无虚构、无主观评价。

**5. 多源交叉验证机制**  
依据知识库规则对代币消息进行来源验证和内容一致性比对，提高信息可信度。


## 项目结构

```
/agent-dropverse
├── character.json               # Agent 性格与语气设定
├── knowledge/
│   ├── tge_basics.txt           # TGE 基础概念知识
│   ├── fake_airdrop_warnings.txt  # 钓鱼空投识别规则
│   ├── claim_pattern_checklist.txt # Claim 页面上线前信号
│   ├── alpha_crosscheck_rules.txt # 多源验证标准
│   └── verified_kol_list.txt     # 可引用账号名单
├── packages/
|   ├── client-twitter            # 处理Agent在Twitter上的执行动作
|   ├── rootdata                  # 爬起Rootdata上的项目方数据
|   ├── plugin-image              # 支持阅读图片的能力

```

## 数据来源
- Twitter账户（官方项目账号、KOL）
- Rootdata的项目方名单


## 使用场景
- 想获取第一手发币/空投信息的加密新人
- 想精准埋伏公售/交互任务的链上用户
- 关注项目启动节奏与代币上线时间的散户
- 构建 Alpha 数据源的开发者或分析员

## 技术栈
- Eliza OS v0.25.9
- Node 23.3 + Typescript
- Twitter 插件（agent-twitter-client）
- JSON

## 整体流程
```mermaid
flowchart TD
    Start([搜索关键字，包括Web3项目方])
    
    F1[每10~15分钟，抓取最Top的前30个推文]
    F2[每5~10分钟，抓取最近的前15个推文]
    Verify1[大模型验证内容与数据，找出相关性最大的文章内容]
    Verify2[根据推文浏览量和点赞数的数量大，浏览量优先级大于点赞数]
    PostType{内容类型}
    A1[空投教程/新闻 → 转发并总结]
    A3[公售项目/TGE → 发布推文，会安全提示]
    End([发布内容])

    Start --> F1
    Start --> F2
    F1 --> Verify1 -- 是 --> PostType
    F2 --> Verify2 -- 是 --> PostType
    PostType --> A1 --> End
    PostType --> A3 --> End
    Verify1 -- 否 --> Start
    Verify2 -- 否 --> Start
```

## DEMO视频/图片


## 免责声明
Drop Verse 仅发布可验证信息，不提供财务建议、不预测市场走势、不转发虚假内容。所有用户请自行判断与研究（DYOR）。

