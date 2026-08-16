# images/ — 照片目录

## 这个目录是空的,需要你自己填充

把你要展示的照片放到这里,推荐命名:

```
images/
├── letter.jpg       对方写给你的手写信(第 1 件礼物)
├── gift-02.jpg      第 2 件礼物
├── gift-03.jpg      第 3 件礼物
├── gift-04.jpg      第 4 件礼物
├── gift-05.jpg      第 5 件礼物
├── gift-06.jpg      第 6 件礼物
├── gift-07.jpg      第 7 件礼物
├── gift-08.jpg      第 8 件礼物
└── gift-09.jpg      第 9 件礼物(高潮页 - 520 名字)
```

## 推荐规格

| 项目 | 建议 |
|------|------|
| 尺寸 | 1080 像素宽(手机端),2160 像素宽(@2x 桌面端) |
| 格式 | jpg(兼容性最好)/ webp(体积更小) |
| 大小 | 单张 < 500 KB |
| 比例 | 竖版(3:4)最佳,适配手机端阅读 |

## ⚠️ 隐私提醒

- **不要 commit 真实的手写信扫描件** 到公开仓库
- 如果你想保留私人版本,可以 fork 一份,把照片放到 `images/` 后私有部署
- 本项目仓库的 `images/` 应该**保持空**,让使用者自己填

## 如何批量压缩

如果你的照片很大,可以用 Python PIL 压缩:

```python
from PIL import Image
import os

for f in os.listdir('images'):
    if not f.endswith('.jpg'): continue
    im = Image.open(f'images/{f}').convert('RGB')
    w, h = im.size
    if w > 1080:
        im = im.resize((1080, int(h*1080/w)), Image.LANCZOS)
    im.save(f'images/{f}', 'JPEG', quality=82, optimize=True)
```

或者在线工具:
- [squoosh.app](https://squoosh.app/)
- [tinypng.com](https://tinypng.com/)