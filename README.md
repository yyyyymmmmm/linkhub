# 🚀 LinkHub - 简洁高效的网址导航系统

[![PHP Version](https://img.shields.io/badge/PHP-%3E%3D7.4-blue)](https://php.net/)
[![MySQL](https://img.shields.io/badge/MySQL-5.7%2B-orange)](https://mysql.com/)
[![SQLite](https://img.shields.io/badge/SQLite-3.0%2B-green)](https://sqlite.org/)
[![License](https://img.shields.io/badge/License-MIT-red)](LICENSE)

## 📖 项目介绍

LinkHub 是一个现代化的网址导航系统，支持多主题、多用户、点击统计、过渡页面等功能。采用PHP原生开发，轻量级且易于部署。

### ✨ 核心特性

- 🎨 **多主题支持** - 内置多套精美主题，支持自定义
- 📊 **点击统计** - 详细的访问统计和数据分析
- 🔄 **过渡页面** - 可选的跳转过渡页，支持广告展示
- 👥 **多用户管理** - 完善的用户权限系统
- 📱 **响应式设计** - 完美适配桌面和移动设备
- 🚀 **开箱即用** - 零配置，自动适配Apache/nginx
- 🔍 **智能搜索** - 支持链接快速搜索和分类
- 💾 **双数据库支持** - MySQL/SQLite任意选择

### 🌟 技术亮点

- **零配置路由** - 自动适配各种服务器环境
- **智能安装** - 支持覆盖安装，避免重复数据
- **主题系统** - 插件化主题架构，易于扩展
- **API接口** - 完整的RESTful API支持
- **安全防护** - XSS防护、CSRF保护、SQL注入防护

## 🛠 环境要求

### 基础环境
- **PHP**: 7.4+ (推荐 8.0+)
- **Web服务器**: Apache 2.4+ / nginx 1.18+
- **数据库**: MySQL 5.7+ / MariaDB 10.3+ / SQLite 3.0+

### PHP扩展
- `PDO` - 数据库连接
- `json` - JSON数据处理  
- `mbstring` - 多字节字符串处理
- `openssl` - 加密功能
- `curl` - HTTP请求（可选）
- `gd` / `imagick` - 图像处理（可选）

### 服务器要求
- 磁盘空间：最少 50MB
- 内存：最少 128MB
- 支持URL重写（推荐）

## 📦 快速安装

### 1. 下载源码

```bash
# 方式1：直接下载
wget https://github.com/your-repo/linkhub/releases/latest/download/linkhub.zip
unzip linkhub.zip

# 方式2：Git克隆
git clone https://github.com/your-repo/linkhub.git
cd linkhub
```

### 2. 配置Web服务器

#### Apache用户（推荐）
✅ **无需配置** - 项目自带`.htaccess`文件，开箱即用

#### nginx用户
在宝塔面板或服务器配置中添加：

**宝塔面板操作：**
1. 网站 → 设置 → 伪静态
2. 添加以下配置：
```nginx
location / {
    try_files $uri $uri/ /index.php?$query_string;
}
```

**手动配置：**
```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /path/to/linkhub/public;
    index index.php index.html;
    
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    
    location ~ \.php$ {
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

### 3. 运行安装程序

1. 浏览器访问：`http://your-domain.com/install.php`
2. 按向导完成安装：
   - **环境检查** - 自动检测服务器环境
   - **数据库配置** - 支持MySQL/SQLite
   - **管理员设置** - 创建管理员账户
   - **完成安装** - 开始使用

### 4. 开始使用

- 前台访问：`http://your-domain.com/`
- 后台管理：`http://your-domain.com/login.php`

## 🔧 配置说明

### 目录结构
```
linkhub/
├── public/             # Web根目录
│   ├── index.php      # 前台入口
│   ├── install.php    # 安装程序
│   ├── login.php      # 登录页面
│   ├── admin/         # 后台管理
│   ├── themes/        # 主题目录
│   └── .htaccess      # Apache重写规则
├── src/               # 核心代码
├── config/            # 配置文件
├── storage/           # 存储目录
├── database/          # 数据库文件
└── README.md          # 说明文档
```

### 重要配置文件
- `.env` - 环境配置（自动生成）
- `config/database.php` - 数据库配置
- `public/.htaccess` - URL重写规则

## 🎨 主题开发

### 主题结构
```
themes/your-theme/
├── index.php          # 主题模板
├── style.css          # 主题样式
├── script.js          # 主题脚本（可选）
├── theme.json         # 主题配置
└── preview.jpg        # 主题预览图
```

### 主题配置示例
```json
{
    "name": "默认主题",
    "version": "1.0.0",
    "author": "LinkHub",
    "description": "简洁的默认主题",
    "config": {
        "show_search": true,
        "show_stats": false,
        "layout": "grid"
    }
}
```

### 可用变量
- `$site` - 网站配置信息
- `$categories` - 分类数据
- `$links` - 链接数据
- `$theme_config` - 主题配置

## 🔗 URL格式

### 前台路由
- `/` - 首页
- `/click/123` - 点击链接（ID为123）
- `/favicon?url=example.com` - 获取网站图标

### 后台路由
- `/admin` - 后台首页
- `/admin/links` - 链接管理
- `/admin/categories` - 分类管理
- `/admin/settings` - 系统设置

### API路由
- `/api/links` - 链接API
- `/api/categories` - 分类API
- `/api/clicks/{id}` - 点击统计API

## 📊 功能特性

### 核心功能
- ✅ 链接管理（增删改查）
- ✅ 分类管理（无限层级）
- ✅ 点击统计（详细数据）
- ✅ 用户管理（多角色权限）
- ✅ 主题系统（插件化架构）
- ✅ 搜索功能（全文搜索）
- ✅ 数据导入导出
- ✅ 系统设置（灵活配置）

### 高级功能
- ✅ 过渡页面（支持广告）
- ✅ 图标缓存（自动获取）
- ✅ 备份还原（一键操作）
- ✅ API接口（RESTful）
- ✅ 响应式设计（多端适配）
- ✅ SEO优化（搜索友好）

## 🚨 故障排除

### 常见问题

#### 1. 点击链接显示404
**原因**: nginx服务器未配置URL重写
**解决**: 在宝塔面板添加伪静态规则：
```nginx
location / {
    try_files $uri $uri/ /index.php?$query_string;
}
```

#### 2. 安装时提示用户名已存在
**原因**: 数据库中已有数据
**解决**: 使用"重新安装"功能，系统会自动清空旧数据

#### 3. 主题无法切换
**原因**: 主题文件权限问题
**解决**: 确保`public/themes/`目录可读

#### 4. 图标无法显示
**原因**: 网络问题或权限问题
**解决**: 检查服务器网络连接和缓存目录权限

### 性能优化

1. **启用PHP缓存**（如OPcache）
2. **配置nginx缓存**（静态资源）
3. **使用CDN**（加速访问）
4. **定期清理**（点击日志）

## 🔒 安全建议

1. **定期更新** - 及时更新到最新版本
2. **强密码** - 使用复杂的管理员密码
3. **文件权限** - 合理设置目录权限
4. **HTTPS** - 启用SSL证书
5. **备份** - 定期备份数据
6. **访问控制** - 限制后台访问IP

## 🤝 贡献指南

### 开发环境搭建
```bash
git clone https://github.com/your-repo/linkhub.git
cd linkhub
```

### 代码规范
- 遵循PSR-4自动加载规范
- 使用PSR-12编码风格
- 添加必要的注释和文档

### 提交规范
```
feat: 新功能
fix: 修复问题
docs: 文档更新
style: 代码格式
refactor: 重构代码
test: 测试相关
```

## 📄 开源协议

本项目基于 [MIT License](LICENSE) 开源协议。

## 🙏 致谢

感谢所有为LinkHub项目贡献代码、提出建议和报告问题的开发者！

## 📞 支持与反馈

- 🐛 **问题反馈**: [GitHub Issues](https://github.com/your-repo/linkhub/issues)
- 💡 **功能建议**: [GitHub Discussions](https://github.com/your-repo/linkhub/discussions)
- 📧 **联系邮箱**: support@linkhub.com
- 💬 **QQ群**: 123456789

---

⭐ 如果这个项目对你有帮助，请给个Star支持一下！

[![Star History Chart](https://api.star-history.com/svg?repos=your-repo/linkhub&type=Date)](https://star-history.com/#your-repo/linkhub&Date)