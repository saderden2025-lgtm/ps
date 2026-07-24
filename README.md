# 🎮 PS Store Tournament Manager (PS店赛事管理系统)

> ⚠️ **LICENSE NOTICE / 许可声明**  
> This project is licensed under the **Functional Source License 1.1 (FSL-1.1)**.  
> ✅ Free for: Personal learning, portfolio display, non-production testing.  
> ❌ Prohibited: Commercial use, production deployment for any business, SaaS offering.  
> 💼 For commercial licensing inquiries, please contact: [你的邮箱/微信]

[![Tech Stack](https://img.shields.io/badge/Stack-UniApp_+_Vue3_+_Node.js-blue)]()
[![License](https://img.shields.io/badge/License-FSL--1.1-orange)]()

## 📖 项目简介

本项目是一套专为 **线下 PlayStation 体验店 / 电竞馆** 设计的赛事数字化解决方案。  
旨在解决传统线下比赛中「纸质报名效率低、比分记录易出错、赛程展示不直观」等痛点，实现从线上报名到线下执裁的全流程数字化管理。

### ✨ 核心功能

| 模块 | 功能点 | 说明 |
|------|--------|------|
| 📱 C端小程序 | 在线报名 | 选手扫码填写信息、选择参赛项目、支付报名费 |
| 📱 C端小程序 | 赛程查看 | 实时对阵图、比分直播、晋级状态推送 |
| 💻 Web管理端 | 赛事创建 | 自定义比赛规则、分组抽签、赛程编排 |
| 💻 Web管理端 | 现场执裁 | 裁判快捷记分、胜负判定、异常申诉处理 |
| 💻 Web管理端 | 数据看板 | 报名人数统计、营收报表、历史赛事归档 |

## 🏗️ 技术架构

- **前端 (C端)**: UniApp + Vue3 + Pinia (编译为微信小程序)
- **前端 (管理端)**: Vue3 + Element Plus + Vite
- **后端**: Node.js (NestJS / Express) + MySQL + Redis
- **部署**: Docker + Nginx + 阿里云OSS (图片存储)
- **其他**: 微信支付API、微信小程序订阅消息

## 🚀 本地开发

```bash
# 克隆项目
git clone https://github.com/your-username/ps-tournament.git

# 安装依赖 & 启动
cd ps-tournament && npm install
npm run dev
