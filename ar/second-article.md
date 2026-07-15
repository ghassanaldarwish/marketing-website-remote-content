---
title: "الأنظمة الخلفية المعتمدة على الأحداث"
description: "استخدام الاتصال غير المتزامن لبناء أنظمة أكثر قابلية للتوسع."

category: "هندسة الأنظمة الخلفية"
status: "دليل"

publishedAt: "2026-07-15"

coverImage: "https://raw.githubusercontent.com/ghassanaldarwish/marketing-website-remote-content/main/assets/articles/dark_logo_500_180.png"
coverImageAlt: "الأنظمة الخلفية المعتمدة على الأحداث"

tags:
  - "Backend"
  - "Kafka"

stack:
  - "Node.js"
  - "Kafka"

draft: false
---

# الأنظمة الخلفية المعتمدة على الأحداث

تواجه الأنظمة المتزامنة صعوبة في التوسع مع زيادة عدد الطلبات.

من أهم المزايا:

- قابلية توسع أفضل
- تحمل أعلى للأخطاء
- استقلالية الخدمات

```js
publish("user.created", payload);
```
