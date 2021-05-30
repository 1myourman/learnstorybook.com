---
title: 'الإضافات'
tocTitle: 'الإضافات'
description: 'تعلم كيفية دمج و إستخدام إضافات ضبط مشهورة'
commit: 'a23f4d0'
---

<div style="direction: rtl">

يمتلك ستوريبوك نظام بيئي قوي من [الإضافات](https://storybook.js.org/docs/react/configure/storybook-addons) التي يمكنك إستخدامها لتحسين تجربة المطور لكل شخص من فريقك. إطلع عليهم كلهم [هنا](https://storybook.js.org/addons).

إذا كنت تتابع هذه الدروس فقد قابلت بالفعل مجموعة من الإضافات و أعددت إحداها في فصل [الإختبار](/intro-to-storybook/react/en/test/)

## ما هي الضوابط؟

الضوابط Controls تسمح للمصممين و المطورين إكتشاف سلوك المكون بسهولة عن طريق التلاعب في حججها أو براهينها. لا حاجة للكود. الضوابط تُنشئ لوحة إضافات بجانب ستوريز خاصتك, لكي تتمكن من تعديل حججها مباشرةً

الضوابط تأتي جاهزة عند تثبيت ستوريبوك لأول مرة. لا حاجة لأي تهيئة.

<video autoPlay muted playsInline loop>
  <source
    src="/intro-to-storybook/controls-in-action.mp4"
    type="video/mp4"
  />
</video>

## الإضافات تفتح مسارات عمل ستوريبوك جديدة

ستوريبوك [بيئة تطوير مبنية على المكون](https://www.componentdriven.org/) رائعة. إضافة الضوابط تجعل من ستوريبوك أداة توثيق تفاعلية.

### إستخدام الضوابط لإيجاد الحالات الطرفية

بإستخدام الضوابط يكمن لمهندسي ضمان الجودة, مهندسي الواجهات, أو أي صاحب مصلحة من دفع المكون لأقصى حد! لنأخذ في عين الإعتبار المثال التالي, ماذا سيحدث لـ `Task` إذا ضفنا نص **كبير**؟

![أوه لا! المحتوى في الجهة اليمنى مقطوع!](/intro-to-storybook/task-edge-case.png)

هذا ليس صحيحا! يبدو أن النص يفيض خارج حدود مكون Task

الضوابط تمكنك من التأكد بسرعة من مدخلات مكون. في هذه الحالة نص طويل. هذا يقلل مقدار العمل المٌتطلب للإكتشاف مشاكل الواجهات.

لنقم الآن بإصلاح مشكلة الفيضان بإضافة نمط لـ `Task.js`:

<div style="direction: ltr">

```diff:title=src/components/Task.js
<input
  type="text"
  value={title}
  readOnly={true}
  placeholder="Input title"
+ style={{ textOverflow: 'ellipsis' }}
/>
```

</div>

![هذا أفضل](/intro-to-storybook/edge-case-solved-with-controls.png)

حُلّت المشكلة. يُقطع النص الآن عند وصوله لحدود Task بإستخدام قطع جميل.

### أضف ستوري جديدة لتفادي التراجع

يمكننا مستقبلاً إعادة إنتاج هذه المشكلة بإدخال نفس النص عن طريق الضوابط. و لكن سيكون أسهل كتابة ستوري تظهر هذه الحالة الطرفية. هذا سيوسع مساحة تخطية إختبار التراجع خاصتنا و يبين حدود المكونات لباقي الفريق.

أضف ستوري جديد من أجل حالة النص الطويل في `Task.stories.js`:

<div style="direction: ltr">

```js:title=src/components/Task.stories.js
const longTitleString = `This task's name is absurdly large. In fact, I think if I keep going I might end up with content overflow. What will happen? The star that represents a pinned task could have text overlapping. The text could cut-off abruptly when it reaches the star. I hope not!`;

export const LongTitle = Template.bind({});
LongTitle.args = {
  task: {
    ...Default.args.task,
    title: longTitleString,
  },
};
```

</div>

يمكننا الآن إعادة إنتاج و العمل على هذه الحالة الطرفية بكل سهولة

<video autoPlay muted playsInline loop>
  <source
    src="/intro-to-storybook/task-stories-long-title.mp4"
    type="video/mp4"
  />
</video>

إذا قمنا [بالإختبار الظاهري](/intro-to-storybook/react/en/test/) سيتم إعلامنا أيضا عند تعطل حل القطع. تكون الحالات الطرفية الغامضة عرضةََ للنسيان إذا لم يغطيها إختبار.

<div class="aside"><p>💡 تعتبر الضوابط طريقة رائعة لتمكين غير-المطورين من التلاعب بالمكونات و الستوريز, إضافةً إلى أشياء أخرى لم نرها هنا, نوصي بقراءة <a href="https://storybook.js.org/docs/react/essentials/controls">التوثيق الرسمي</a> لمعرفة المزيد. و لكن يوجد العديد من الطرق لتعديل ستوريبوك ليناسب مسار عملك و إضافاتك. في <a href="/create-an-addon/react/en/introduction/">دليل إنشاء إضافة</a> سنعلمك أنه بإنشائك لإضافة, يساعدك ذلك على تحسين مسار تطويرك.</p></div>

### إدمج التغييرات

لا تنسى دمج تغييراتك مع git!

</div>
