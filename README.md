# Taiba Academy — Smart Academic Assistant

مساعد أكاديمي ذكي بالعربية لطلاب معهد طيبة العالي لتكنولوجيا الإدارة والمعلومات (فرع الجيزة).
واجهة محادثة PWA تعتمد على **قاعدة معرفة محلية**، مع طبقة **Gemini** آمنة تعمل عبر Vercel Serverless Function. لو تعطل الذكاء الاصطناعي، يكمل الموقع الإجابة من قاعدة المعرفة.

> مشروع شخصي — تصميم وتطوير: **Kyrillos Ayman (كيرلس أيمن)**. ليس موقعًا رسميًا للمعهد.

## المميزات

- شات عربي (RTL) مع اقتراحات ذكية، إكمال تلقائي، وإجابات بمصادر.
- **قاعدة معرفة محلية** تعمل بدون إنترنت أو بدون مفتاح API.
- **طبقة Gemini** تصيغ الرد من قاعدة المعرفة فقط (بدون اختراع معلومات) مع تحديد معدل الطلبات لكل IP.
- **إدخال صوتي ذكي**: سجّل سؤالك بالميكروفون فيفرّغه Gemini (يفهم العامية المصرية) ويجيب تلقائيًا.
- **رفع ملفات**: صور، PDF (حتى 3MB)، Word (.docx)، txt/md/csv، ويجيب Gemini من محتواها. الميزتان تحتاجان Vercel + مفتاح Gemini وHTTPS.
- PWA قابل للتثبيت، وService Worker يعمل بنمط network-first.
- جدول محاضرات، حاسبة معدل تراكمي، تقويم أكاديمي، نظام تذاكر محلي، وتحليلات محفوظة في `localStorage`.
- الأمان: مفتاح Gemini على الخادم فقط، وترويسات أمان في `vercel.json`.

## التقنيات

HTML / CSS / JavaScript (بدون framework) · Vercel Serverless (Node 20+) · Gemini API · PWA

## هيكل المشروع

```
index.html        الواجهة + قاعدة المعرفة + منطق الشات
api/chat.js       Serverless Function تستدعي Gemini من الخادم
sw.js             Service Worker
manifest.json     إعدادات PWA
icon*.png/svg     الأيقونات
vercel.json       مهلة الدالة + ترويسات الأمان
.env.example      أسماء متغيرات البيئة
```

## التشغيل المحلي (مع Gemini)

1. ثبّت Node.js 20+ وVercel CLI: `npm i -g vercel`
2. انسخ `.env.example` إلى `.env.local` وضع مفتاحك من https://aistudio.google.com/apikey
3. شغّل `npm run dev` (أول مرة سيطلب منك `vercel login` وربط المشروع) ثم افتح الرابط.

> فتح `index.html` مباشرة يعمل بقاعدة المعرفة المحلية فقط لأن `/api/chat` غير متاح.

## النشر على Vercel

1. من https://vercel.com اختر **Add New → Project** واستورد المستودع.
2. في **Settings → Environment Variables** أضف `GEMINI_API_KEY` (و`GEMINI_MODEL` اختياري، الافتراضي `gemini-3.8-flash`).
3. اضغط **Deploy**، وبعد أي تغيير في المتغيرات اعمل **Redeploy**.

GitHub Pages يعرض الموقع بقاعدة المعرفة المحلية فقط (بدون Gemini).

## ملاحظات

- عند تعديل ملفات الواجهة ارفع رقم `CACHE` في `sw.js`.
- بعد النشر ضع رابطًا كاملًا في `og:image` داخل `index.html`.
- المحادثات والتذاكر محفوظة على جهاز المستخدم فقط. الرسوم والمواعيد في قاعدة المعرفة قد تحتاج مراجعة رسمية.

## الترخيص

MIT © 2026 Kyrillos Ayman
