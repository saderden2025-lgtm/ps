# PS游戏厅 赛事管理系统

## 项目概述

为PS游戏厅(实况足球)设计的完整赛事管理系统，包含：
- **微信小程序**：玩家端，支持查看赛事、报名参赛、查看积分榜/对阵
- **后台管理系统**：管理员端，支持创建赛事、录入比分、发布公告
- **后端API服务**：Node.js + Express + PostgreSQL

## 技术栈

| 模块 | 技术 |
|------|------|
| 后端 | Node.js + Express + PostgreSQL + JWT |
| 后台管理 | Vue 3 + Element Plus + Vite + Pinia |
| 小程序 | 微信小程序原生开发 |
| 数据库 | PostgreSQL |

## 项目结构

```
ps/
├── server/                    # 后端服务
│   ├── src/
│   │   ├── app.js            # 入口文件
│   │   ├── config/db.js      # 数据库配置
│   │   ├── middleware/auth.js # 认证中间件
│   │   ├── controllers/       # 控制器
│   │   │   ├── authController.js
│   │   │   ├── tournamentController.js
│   │   │   ├── matchController.js
│   │   │   ├── standingController.js
│   │   │   └── announcementController.js
│   │   └── routes/index.js    # 路由配置
│   ├── database/schema.sql    # 数据库建表脚本
│   ├── .env                   # 环境变量
│   └── package.json
├── admin/                     # 后台管理系统
│   ├── src/
│   │   ├── main.js           # Vue入口
│   │   ├── App.vue
│   │   ├── router/index.js   # 路由配置
│   │   ├── stores/auth.js    # 状态管理
│   │   ├── api/index.js      # API封装
│   │   └── views/
│   │       ├── Login.vue      # 登录页
│   │       ├── Layout.vue     # 布局组件
│   │       ├── Dashboard.vue  # 仪表盘
│   │       ├── tournaments/   # 赛事管理
│   │       │   ├── List.vue
│   │       │   ├── Create.vue
│   │       │   ├── Detail.vue
│   │       │   └── MatchManagement.vue
│   │       └── announcements/ # 公告管理
│   │           ├── List.vue
│   │           └── Create.vue
│   ├── vite.config.js
│   └── package.json
├── miniprogram/              # 微信小程序
│   ├── app.js
│   ├── app.json
│   ├── utils/api.js         # API封装
│   └── pages/
│       ├── index/            # 首页-赛事列表
│       ├── tournament/
│       │   ├── detail        # 赛事详情+报名
│       │   ├── standings     # 积分榜
│       │   └── matches       # 比赛对阵
│       ├── announcement/detail # 公告详情
│       └── mine/
│           ├── index         # 个人中心
│           └── enrollments   # 我的报名
└── README.md
```

## 快速开始

### 1. 数据库初始化

```bash
# 创建数据库
createdb ps_game_hall

# 执行建表脚本
psql -U postgres -d ps_game_hall -f server/database/schema.sql
```

### 2. 后端启动

```bash
cd server
npm install

# 编辑 .env 文件，配置数据库连接等信息
# DB_HOST=localhost
# DB_PORT=5432
# DB_USER=postgres
# DB_PASSWORD=your_password
# DB_NAME=ps_game_hall

npm run dev
# 服务启动在 http://localhost:3000
```

### 3. 后台管理启动

```bash
cd admin
npm install
npm run dev
# 访问 http://localhost:5173
# 默认账号: admin / admin123
```

### 4. 小程序启动

1. 下载并打开 [微信开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)
2. 导入项目，选择 `miniprogram/` 目录
3. 填写小程序 AppID
4. 修改 `utils/api.js` 中的 `BASE_URL` 为实际后端地址

## 核心功能说明

### 赛事模式

#### 积分小组赛 + 淘汰赛 (group_knockout)
1. 管理员创建赛事，设置小组数量、每组人数、晋级人数
2. 报名截止后，系统自动随机分组
3. 每组内进行单循环比赛
4. 小组赛结束后，每组前N名晋级淘汰赛
5. 淘汰赛：16强 → 8强 → 半决赛 → 决赛

#### 联赛制 (league)
1. 最少20人参赛
2. 支持单循环/双循环(主客场)
3. 所有选手相互对阵
4. 系统使用循环赛算法自动生成完整赛程
5. 按积分排名：胜3分、平1分、负0分

### 比分录入与积分计算

- 管理员录入比分后，系统自动：
  1. 更新比赛状态为"已结束"
  2. 更新积分榜(胜场、平局、负场、进球、失球、净胜球、积分)
  3. 自动计算排名
  4. 淘汰赛模式自动生成下一轮对阵

### 小程序功能

| 页面 | 功能 |
|------|------|
| 首页 | 赛事列表、轮播广告、筛选(模式/状态) |
| 赛事详情 | 赛事信息、报名选手、报名参赛 |
| 积分榜 | 小组积分/联赛积分、实时排名 |
| 比赛对阵 | 所有比赛对阵和比分 |
| 我的 | 个人信息、报名记录、PSN设置 |
| 公告 | 赛事广告/通知查看 |

### 后台管理功能

| 页面 | 功能 |
|------|------|
| 仪表盘 | 赛事统计、快捷操作 |
| 赛事列表 | 管理所有赛事、变更状态 |
| 创建赛事 | 创建杯赛/联赛、配置规则 |
| 赛事详情 | 查看报名、积分榜 |
| 比分管理 | 添加对阵、录入比分、自动生成赛程 |
| 公告管理 | 发布/编辑/删除公告和广告 |

## API 接口概览

| 方法 | 路径 | 说明 |
|------|------|------|
| POST | /api/auth/wx-login | 微信登录 |
| PUT | /api/user/profile | 更新个人信息 |
| POST | /api/admin/login | 管理员登录 |
| GET | /api/tournaments | 赛事列表 |
| GET | /api/tournaments/:id | 赛事详情 |
| POST | /api/tournaments/:id/enroll | 报名参赛 |
| GET | /api/tournaments/:id/standings | 获取积分榜 |
| GET | /api/tournaments/:id/matches | 获取对阵 |
| POST | /api/admin/tournaments | 创建赛事 |
| PUT | /api/admin/matches/:id/score | 录入比分 |
| POST | /api/admin/matches/generate-group | 生成小组赛对阵 |
| POST | /api/admin/matches/generate-league | 生成联赛对阵 |
| GET/POST | /api/admin/announcements | 公告管理 |

## 注意事项

1. 小程序需在微信公众平台注册并获取 AppID
2. 生产环境请修改 JWT_SECRET 和数据库密码
3. 图片上传需要配置云存储(如腾讯云COS)
4. 微信支付(报名费)需要单独对接微信支付API
5. 首次使用请先在数据库中执行 schema.sql
