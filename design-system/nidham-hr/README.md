# نظام تصميم نِظام (Nidham HR Design System)

دليل سريع لمحتويات المجلد:

| الملف / المجلد | الوصف |
|---|---|
| `MASTER.md` | المرجع المولّد من محرك ui-ux-pro-max (ستايل، ألوان، قواعد) — بالإنجليزية |
| `brand-guidelines-ar.md` | **دليل الهوية البصرية الكامل بالعربي** — ابدأ من هنا |
| `tokens/design-tokens.json` | توكنز التصميم بصيغة JSON (طبقات primitive → semantic → component) |
| `tokens/tokens.css` | نفس التوكنز كمتغيرات CSS جاهزة للاستخدام (فاتح + غامق + RTL) |
| `website-ux-review-ar.md` | تقرير مراجعة UX لموقع nidhamhr.com (نتائج + تشيك ليست) |
| `marketing/hero/index.html` | سكشن الهيرو للموقع — RTL كامل بالتوكنز |
| `marketing/banners/banner-1200x628.html` | بانر إعلان Facebook / LinkedIn |
| `marketing/banners/banner-1080x1080.html` | بانر مربع Instagram / Facebook |
| `marketing/previews/*.png` | معاينات جاهزة للمشاركة من كل التصميمات |
| `pages/` | Overrides لصفحات معينة (فاضي حالياً — بيتقري قبل MASTER.md) |

## الاستخدام في أي واجهة جديدة

```html
<link rel="stylesheet" href="design-system/nidham-hr/tokens/tokens.css">
```

وبعدها استخدم المتغيرات (`var(--color-primary)`، `var(--space-4)`...) بدل أي قيم مباشرة.
لتعديل البانرات: افتح ملف الـ HTML، عدّل النصوص، وصوّره بأي متصفح على نفس مقاس الصفحة.
