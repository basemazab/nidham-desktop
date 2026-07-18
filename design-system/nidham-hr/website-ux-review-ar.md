# مراجعة UX لموقع nidhamhr.com — التقرير الأولي

**التاريخ:** 18 يوليو 2026 · **المرجعية:** قواعد UX (98 قاعدة، ui-ux-pro-max v2.11) + دليل هوية نِظام v1.0

---

## ملخص تنفيذي

المراجعة البصرية الكاملة **متوقفة مؤقتاً على الوصول للموقع** (راجع «حدود المراجعة» تحت)، لكن الفحص التقني كشف **نتيجتين مؤكدتين عالييتَي الأولوية** لازم يتصلحوا بغض النظر عن أي حاجة تانية:

### 🔴 النتيجة 1: تحليلات الموقع صفر — بتطير من غير عدادات

استعلمنا PostHog المربوط بحساب Nidhamhr (Project 511339) عن آخر 30 يوم:

| المقياس | القيمة |
|---|---|
| الزوار | **0** |
| مشاهدات الصفحات | **0** |
| الجلسات | **0** |

**المعنى:** كود تتبع PostHog **مش متركّب على nidhamhr.com أصلاً** (أو بيبعت لمشروع تاني). أي قرار تسويقي أو UX دلوقتي بيتاخد من غير أي بيانات.

**الإصلاح (15 دقيقة):** تركيب snippet الخاص بالمشروع في `<head>` بتاع الموقع:

```html
<script>
  !function(t,e){var o,n,p,r;e.__SV||(window.posthog=e,e._i=[],e.init=function(i,s,a){function g(t,e){var o=e.split(".");2==o.length&&(t=t[o[0]],e=o[1]),t[e]=function(){t.push([e].concat(Array.prototype.slice.call(arguments,0)))}}(p=t.createElement("script")).type="text/javascript",p.crossOrigin="anonymous",p.async=!0,p.src=s.api_host.replace(".i.posthog.com","-assets.i.posthog.com")+"/static/array.js",(r=t.getElementsByTagName("script")[0]).parentNode.insertBefore(p,r);var u=e;for(void 0!==a?u=e[a]=[]:a="posthog",u.people=u.people||[],u.toString=function(t){var e="posthog";return"posthog"!==a&&(e+="."+a),t||(e+=" (stub)"),e},u.people.toString=function(){return u.toString(1)+".people (stub)"},o="init capture register register_once register_for_session unregister unregister_for_session getFeatureFlag getFeatureFlagPayload isFeatureEnabled reloadFeatureFlags updateEarlyAccessFeatureEnrollment getEarlyAccessFeatures on onFeatureFlags onSurveysLoaded onSessionId getSurveys getActiveMatchingSurveys renderSurvey canRenderSurvey canRenderSurveyAsync identify setPersonProperties group resetGroups setPersonPropertiesForFlags resetPersonPropertiesForFlags setGroupPropertiesForFlags resetGroupPropertiesForFlags reset get_distinct_id getGroups get_session_id get_session_replay_url alias set_config startSessionRecording stopSessionRecording sessionRecordingStarted captureException loadToolbar get_property getSessionProperty createPersonProfile opt_in_capturing opt_out_capturing has_opted_in_capturing has_opted_out_capturing clear_opt_in_out_capturing debug getPageViewId captureTraceFeedback captureTraceMetric".split(" "),n=0;n<o.length;n++)g(u,o[n]);e._i.push([i,s,a])},e.__SV=1)}(document,window.posthog||[]);
  posthog.init('phc_DcdHLSup3gbHKTAZQUqZWMCQxrTrE36jS4azffn7jjjV', {
    api_host: 'https://us.i.posthog.com',
    defaults: '2025-05-24'
  });
</script>
```

وبعد التركيب، فعّل: **Session recordings** (تسجيل جلسات الزوار = مراجعة UX حقيقية مستمرة) + حدد **هدفي تحويل**: الضغط على زر تحميل التطبيق، وإرسال فورم التواصل/طلب الديمو.

### 🟠 النتيجة 2: الموقع بيرد 403 على العملاء الآليين — افحص وصول محركات البحث

كل محاولات الوصول الآلية للموقع (من أكتر من مسار) رجعت **HTTP 403 Forbidden**. لو الـ WAF/الحماية بتحجب بوتات محركات البحث بنفس الطريقة، الموقع **ممكن ميتفهرسش في جوجل خالص**.

**الفحص (10 دقائق):**
1. افتح [Google Search Console](https://search.google.com/search-console) → Pages → شوف عدد الصفحات المفهرسة وأخطاء الزحف.
2. جرّب في جوجل: `site:nidhamhr.com` — لو النتائج قليلة أو مفيش، المشكلة مؤكدة.
3. لو مؤكدة: ظبّط قواعد الـ WAF (Cloudflare أو غيره) تسمح لـ Googlebot و Bingbot المُتحقق منهم.

---

## حدود المراجعة الحالية

البيئة السحابية اللي شغال منها محجوب عنها nidhamhr.com (سياسة شبكة + WAF الموقع). عشان أكمّل **المراجعة البصرية التفصيلية** محتاج واحدة من دول:

1. **سكرين شوتس** من الموقع (ديسكتوب + موبايل) ومن شاشات التطبيق الرئيسية — ابعتهم في الشات وأنا أراجعهم فوراً ضد الـ 98 قاعدة، أو
2. إضافة `nidhamhr.com` لقائمة النطاقات المسموحة في إعدادات بيئة Claude Code (Environment → Network policy).

## تشيك ليست المراجعة الجاهزة (هتتطبق فور توفر الوصول)

مرتّبة بالأولوية — دي نفسها اللي هقيّم بيها كل صفحة/شاشة:

### P1 — حرِج
- [ ] تباين النصوص ≥ 4.5:1 (خصوصاً النص الرمادي على خلفيات فاتحة)
- [ ] كل الصور فيها `alt` وصفي بالعربي
- [ ] التنقل بالكيبورد شغال وfocus ظاهر
- [ ] أهداف النقر ≥ 44×44px في الموبايل
- [ ] زر CTA واحد واضح فوق الطية (تحميل التطبيق أو اطلب ديمو — مش الاتنين بنفس الوزن)

### P2 — عالي
- [ ] `<html dir="rtl" lang="ar">` والمحاذاة يمين متسقة في كل الصفحات
- [ ] الهيرو بيجاوب في 5 ثواني: بيعمل إيه؟ لمين؟ أعمل إيه دلوقتي؟
- [ ] إشارات ثقة: لوجوهات عملاء / أرقام (عدد شركات، موظفين بيتداروا) / شهادات
- [ ] الموقع responsive على 375px من غير سكرول أفقي
- [ ] سرعة التحميل: صور WebP/AVIF + lazy loading (افحص بـ PageSpeed Insights)

### P3 — متوسط
- [ ] الخطوط: عناوين Cairo ونصوص IBM Plex Sans Arabic (حسب دليل الهوية) — مش أكتر من خطين
- [ ] النص الأساسي ≥ 16px وارتفاع السطر ≥ 1.6
- [ ] فورم التواصل: labels ظاهرة، أخطاء جنب الحقول، `type="tel"` للموبايل
- [ ] صفحة تسعير واضحة أو CTA «اطلب عرض سعر» صريح
- [ ] Footer فيه: تواصل، سياسة خصوصية، روابط سوشيال شغالة

### P4 — تحسينات
- [ ] حركة خفيفة هادفة 150-300ms مع احترام `prefers-reduced-motion`
- [ ] Favicon + Open Graph tags (معاينة الشير على واتساب/فيسبوك)
- [ ] سكشن أسئلة شائعة (بيقلل تردد العميل المصري قبل التواصل)

---

*التقرير هيتحدّث بالمراجعة البصرية الكاملة فور توفر الوصول أو السكرين شوتس.*
