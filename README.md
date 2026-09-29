# DOSH — Production Store

نسخة متجر DOSH مبنية كمتجر Full‑Stack حقيقي باستخدام Next.js + Supabase (Postgres/Auth/Storage) ومهيأة للرفع على استضافة تدعم Node.js مثل Vercel.

## الموجود
- واجهة DOSH عربية RTL متجاوبة مستوحاة من التصميم الذي أرسلته.
- المنتجات من قاعدة بيانات حقيقية.
- تصنيفات، مقاسات، ألوان، مخزون، أسعار، منتجات مميزة.
- صفحة تفاصيل المنتج.
- سلة مشتريات.
- Checkout حقيقي ينشئ الطلب داخل PostgreSQL.
- خصم المخزون داخل transaction في دالة `place_order`.
- لوحة تحكم `/admin` محمية بحساب Supabase Auth ودور admin.
- إضافة/تعديل/حذف/إخفاء المنتجات.
- رفع صور المنتجات إلى Supabase Storage.
- إدارة حالة الطلبات.
- Row Level Security (RLS) لحماية البيانات.
- زر واتساب للتواصل.

## تشغيل محلي
```bash
npm install
cp .env.example .env.local
npm run dev
```
ثم افتح `http://localhost:3000`.

## إعداد Supabase
1. أنشئ مشروعاً في Supabase.
2. افتح SQL Editor وشغّل كامل الملف `supabase/migrations/001_init.sql`.
3. من Authentication > Users أنشئ مستخدم الإدارة بالبريد وكلمة المرور.
4. في SQL Editor اجعل المستخدم Admin:
```sql
update public.profiles set role='admin' where email='YOUR_ADMIN_EMAIL';
```
5. انسخ Project URL وPublishable Key إلى `.env.local`.

> لا تضع Service Role/Secret key داخل المتصفح أو في متغير يبدأ بـ `NEXT_PUBLIC_`.

## النشر
### Vercel
- ارفع المشروع إلى GitHub.
- Import Project في Vercel.
- أضف:
  - `NEXT_PUBLIC_SUPABASE_URL`
  - `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
- Deploy.
- أضف الدومين الخاص بك إذا أردت.

### استضافة Node.js عادية
```bash
npm install
npm run build
npm start
```

## قبل الإطلاق التجاري
- استبدال صور Unsplash بصور منتجات DOSH.
- ضبط أسعار وشحن واستبدال حقيقية.
- إضافة سياسة الخصوصية والشحن والاسترجاع.
- اختبار الطلبات والمخزون على الهاتف.
- إضافة بوابة دفع محلية إذا أردت الدفع الإلكتروني؛ النسخة الحالية تعتمد على الطلب والدفع عند التنسيق/التسليم.
