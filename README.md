# 照片存储平台

一个现代化、响应式的照片上传和存储管理网站，支持拖拽上传、照片预览、删除和下载功能。

## 功能特性

### 🚀 核心功能
- **拖拽上传**: 支持拖拽文件到指定区域进行上传
- **点击上传**: 点击按钮选择文件上传
- **格式支持**: 支持 JPG、PNG、WebP、GIF 格式
- **文件大小限制**: 单个文件最大 10MB
- **本地存储**: 使用 localStorage 保存照片数据
- **响应式设计**: 完美适配桌面端、平板端和移动端

### 📱 用户界面
- **现代极简设计**: 采用现代极简主义设计风格
- **砌体布局**: 照片网格采用砌体布局，自动适应不同宽高比
- **交互动效**: 流畅的悬停和点击动效
- **预览模态框**: 点击照片可全屏预览
- **操作面板**: 悬停显示文件名和操作按钮

### 🛠️ 管理功能
- **照片预览**: 点击查看大图预览
- **文件信息**: 显示文件名、大小、类型、上传时间
- **下载功能**: 支持单张照片下载
- **删除功能**: 安全删除不需要的照片
- **批量统计**: 实时显示照片总数和存储信息

### 🔧 技术特性
- **离线支持**: 使用 Service Worker 实现离线访问
- **数据持久化**: 照片数据保存在浏览器本地存储
- **性能优化**: 图片懒加载和虚拟滚动
- **错误处理**: 完善的错误处理和用户提示
- **无依赖框架**: 纯原生 JavaScript 实现

## 文件结构

```
photo-storage-website/
├── index.html          # 主页面文件
├── styles.css          # 样式文件
├── script.js           # 功能脚本
├── sw.js              # Service Worker（离线支持）
└── README.md          # 说明文档
```

## 使用方法

### 1. 基本使用
1. 打开 `index.html` 文件
2. 将照片拖拽到上传区域或点击"选择文件"按钮
3. 支持多选文件批量上传
4. 照片将自动显示在网格中

### 2. 照片管理
- **预览**: 点击任意照片查看大图
- **下载**: 在预览模式下点击"下载"按钮
- **删除**: 在预览模式下点击"删除"按钮
- **批量删除**: 依次删除不需要的照片

### 3. 响应式使用
- **桌面端**: 支持拖拽上传，砌体布局显示照片
- **平板端**: 优化的触摸体验和布局
- **移动端**: 单列/双列布局，大尺寸触摸按钮

## 技术栈

- **HTML5**: 语义化标签和现代 API
- **CSS3**: Flexbox、Grid、动画和响应式设计
- **JavaScript ES6+**: 模块化编程和现代语法
- **Lucide Icons**: 现代化图标库
- **Inter 字体**: Google Fonts 提供的现代字体
- **Service Worker**: 离线缓存和 PWA 支持

## 浏览器兼容性

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+

## 存储说明

### 本地存储
- 照片数据存储在浏览器的 localStorage 中
- 存储容量限制约为 5-10MB（取决于浏览器）
- 清除浏览器数据会丢失所有照片

### 数据格式
```javascript
{
  id: "unique-id",
  name: "filename.jpg",
  data: "data:image/jpeg;base64,...", // Base64 编码的图片数据
  type: "image/jpeg",
  size: 1024000,
  uploadDate: "2025-11-22T02:06:57.000Z"
}
```

## 开发指南

### 本地运行
```bash
# 克隆项目到本地
git clone [repository-url]

# 进入项目目录
cd photo-storage-website

# 启动本地服务器（推荐使用 Live Server 扩展）
# 或使用 Python 简单服务器
python -m http.server 8000

# 访问 http://localhost:8000
```

### 自定义配置

#### 修改上传限制
在 `script.js` 中修改以下配置：
```javascript
const maxSize = 20 * 1024 * 1024; // 修改为 20MB
const validTypes = ['image/jpeg', 'image/jpg', 'image/png', 'image/webp', 'image/gif', 'image/bmp'];
```

#### 修改样式主题
在 `styles.css` 中修改 CSS 变量：
```css
:root {
  --primary-color: #007AFF;     /* 修改主色调 */
  --neutral-900: #1D2939;       /* 修改主文本色 */
  --background-color: #F8F9FA;  /* 修改背景色 */
}
```

#### 添加新功能
在 `script.js` 的 `PhotoStorage` 类中添加新方法：
```javascript
// 示例：添加照片重命名功能
renamePhoto(index, newName) {
    if (this.photos[index]) {
        this.photos[index].name = newName;
        this.savePhotos();
        this.renderPhotos();
        this.showToast('照片已重命名');
    }
}
```

## 性能优化

### 1. 图片优化
- 自动压缩大尺寸图片
- 支持 WebP 格式以减少文件大小
- 懒加载机制减少初始加载时间

### 2. 存储优化
- Base64 编码减少存储空间
- 分批处理大量文件上传
- 异步文件读取避免界面卡顿

### 3. 渲染优化
- 虚拟滚动支持大量照片
- CSS 硬件加速动画
- 事件委托减少内存占用

## 常见问题

### Q: 为什么照片上传失败？
A: 请检查：
- 文件格式是否为 JPG、PNG、WebP、GIF
- 文件大小是否超过 10MB
- 浏览器存储空间是否充足

### Q: 照片数据会丢失吗？
A: 照片存储在浏览器本地，清除浏览器数据会丢失。建议定期导出重要照片。

### Q: 如何备份照片？
A: 可以在控制台执行 `window.debugPhotoStorage.exportPhotos()` 导出 JSON 备份文件。

### Q: 支持多少张照片？
A: 取决于浏览器存储空间，一般可存储数百张照片。建议不超过 1000 张以保证性能。

## 许可证

MIT License - 自由使用和修改

## 更新日志

### v1.0.0 (2025-11-22)
- 初始版本发布
- 实现基本的上传、预览、删除功能
- 添加响应式设计和离线支持
- 完成现代化的 UI/UX 设计

---

**作者**: MiniMax Agent  
**技术栈**: HTML5 + CSS3 + JavaScript ES6+  
**最后更新**: 2025-11-22