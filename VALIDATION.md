# 俄罗斯方块 - 验收清单

## 发布前检查

- [x] `index.html` 中文字符正确，无乱码
- [x] `charset=utf-8` 声明存在
- [x] `body { background: #1a1008 }` 存在（非透明）
- [x] 核心循环可触发（← →移动、↑旋转、↓加速、空格落地）
- [x] localStorage 可正常写入（最高分存档）
- [x] 控制台无 Error 级别报错
- [ ] Playwright 测试全通过

## 游戏功能检查

- [x] 方块可左右移动（← →）
- [x] 方块可旋转（↑）
- [x] 方块可加速下落（↓）
- [x] 方块可直接落地（空格）
- [x] 下一个方块预览显示正常
- [x] 消行得分正确（1行100/2行300/3行500/4行800）
- [x] 等级加速正常（每10行升一级）
- [x] 游戏结束判定正确
- [x] 最高分存档（localStorage）
- [x] 幽灵方块显示

## 心跳检查项

每分钟检查：

```javascript
// 1. Pages 可访问
GET 'https://schaezel.github.io/tetris-russia/'
expect: 200 OK

// 2. JS 无语法错误
// 浏览器控制台检查 "Uncaught"

// 3. localStorage 写入正常
localStorage.setItem('tetris_save','{"best":0}')
localStorage.getItem('tetris_save') !== null

// 4. 方块可移动
// 按 ← → 键方块应左右移动

// 5. 中文渲染正确
document.title.includes('俄罗斯方块')
```

## 自动修复触发条件

| 问题 | 条件 | 修复方式 |
|------|------|---------|
| Pages 404 | 持续 2 分钟 | 重新触发 GitHub Pages build |
| 控制台 Error | 任意 | 回滚到上一个稳定 commit |
| 乱码 | 任意 | 重新 encode UTF-8 |
