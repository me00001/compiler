<div dir=rtl>

## The Arabic Programming Language, Alif - لغة البرمجة العربية، ألف

## كيف يعمل مترجم ألف ؟

مترجم ألف يقوم بترجمة لغة ألف إلى لغة سي++ مع استعمال مكتبات [بوست](https://boost.org)

> **_[ ! ] تنبيه_**
>
> مشروع ألف نسخة 3 هو قيد التطوير ولا يصلح حاليا للاستخدام، لكن يمكنك استعمال وتجربة ألف النسخة 2 عبر تحميله من الموقع الرسمي https://aliflang.org

## طريقة ترجمة الشيفرة المصدرية للمشروع

### المتطلبات

1. مترجم مناسب، مثل مترجم gcc الإصدار رقم 8 على الأقل
2. مكتبات بوست، على الأقل الإصدار رقم 1.74

### استنساخ الكود لجهازك

<div dir=ltr>

```bash
git clone --depth=1 -b main --single-branch https://github.com/alifcommunity/compiler.git
cd compiler
mkdir build
cd build
```

</div>

### البناء

للبناء المشروع على أي نظام تشغيل باستخدام `make`

<div dir=ltr>

```bash
make build
```

</div>

#### Windows

البناء باستخدام **_GCC (MinGW64)_**.

<div dir=ltr>

```bash
cmake .. -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Release
mingw32-make
mingw32-make install
```

</div>

البناء باستخدام **_Microsoft build tools 2019_**.

<div dir=ltr>

```bash
cmake .. -G "NMake Makefiles" -DCMAKE_BUILD_TYPE=Release
nmake
```

</div>

#### Linux

تنصيب مترجم GCC & GTK3

<div dir=ltr>

```
sudo apt install build-essential libgtk-3-dev
```

</div>

تنصيب مكتبات Boost +1.74

إن لم تكن موجودة بالفعل في المتسودع الرسمي لحزم توزيعة اللينوكس، قم بتنصيبها يدويا:

<div dir=ltr>

```
wget https://boostorg.jfrog.io/artifactory/main/release/1.76.0/source/boost_1_76_0.tar.gz
tar -xzf boost_1_76_0.tar.gz
cd boost_1_76_0
./bootstrap.sh
sudo ./b2 install address-model=64 variant=release link=shared runtime-link=shared warnings=off --with-filesystem --with-program_options --with-system --with-locale --with-date_time --with-regex --with-nowide --with-thread
```

</div>

بناء مترجم ألف باستخدام GCC.

<div dir=ltr>

```bash
cmake ..
make && sudo make install
```

</div>

## المساهمة في تطوير اللغة

قال صلى الله عليه وسلم : "يد الله مع الجماعة". بدأت اللغة كعمل فردي ومبادرة من حسن دراجة، لكن اللغة تنمو بالمساهمين والمطورين الذي يريدون رؤية اللغة العربية على رأس اللغات وأفضلهم.

### المتطلبات

1. أنت بحاجة لتوفية متطلبات البناء في الجزء الخاص ببناء المترجم، _هذا بديهي_ 😅
2. على الأقل أنت بحاجة لـ "جيت" الإصدار 2.9.0 لاستعمال الخطافات، [المصدر](https://stackoverflow.com/questions/39332407/git-hooks-applying-git-config-core-hookspath)
3. قم بتنصيب clang-format، تأتي ضمن مترجم ال clang
4. مفسر لغة بايثون، حيث يٌتطلب وجود `python`، `pip`، `venv` لإجراء الاختبارات
5. <sub>(خياريا وليس إلزاما)،</sub> لتنسيق ملفات `yaml, json, ...`، يجب توافر أداة prettier التي يمكن تنصيبها من npm والتي تأتي مع ال NodeJs. للتنصيب: `npm i -g prettier`
6. تشغيل الكود الخاص بإعداد المشروع للتطوير، انظر التعليمات بالأسفل

### استنساخ الكود وإعداده

<div dir=ltr>

```
git clone https://github.com/alifcommunity/compiler.git alif-compiler
```

```
python ./إعداد_للتطوير.py
```

</div>

### إجراء الاختبارات

الاختبارات على الكود يتم تنفيذها من خلل كود بايثون، وستكون مستقبلا بلغة ألف إن شاء الله، لذا يتطلب تصطيب بايثون أولا

**لتشغيل الاختبارات**

- يمكنك الإعداد إن لم تكن قد أعددت المشروع للتطوير مسبقا: <span dir=ltr>`python إعداد_للتطوير.py اختبارات`</span> ، أو `make prepare-tests`
- يمكنك أن تشغل الاختبارات من خلال `make tests`

```
> ./اختبارات/اختبر --مساعدة
الاستخدام: اجراء_الاختبارات [--مساعدة] [--تكميل] [--القواعد-فقط] [--تجديد]
                        [--مسار مسار]

إجراء اختبارات لمترجم ألف.

أَسْناد غير إلزامية:
  --مساعدة, -م          احصل على رسالة المساعدة هذه
  --تكميل, -ك           بانتاج ملفات التوقع الغير موجودة من خلال ما يحدث فعلا
                        عند ترجمة وتنفيذ الكود
  --القواعد-فقط, -ق     اختبار القواعد فقط بدون الخَرج أو الترجمة الكاملة
  --تجديد, -ج           إعادة انتاج كل التوقعات من الكود وإهمال القديم. هذه
                        الأمر لابد أن تكون واعيا بتبعاته
  --مسار مسار, -س مسار  تحديد مسار لجمع الاختبارات منه ومن المسارات الفرعية
                        بداخلة
```

**إنشاء اختبارات جديدة**

قم بوضع ملف فيه كود لألف في المسار `./اختبارات/أكواد`، ويمكن وضع ملف الكود في أي مسار فرعي بداخله، كما يمكنك أن تضع المتوقع من الكود في ملف يحمل نفس الإسم وفي نفس المكان مع إضافة `_توقع.yml`

فمثلا لو أردت أن تعمل بال TDD، سنقوم بعمل مثل الختبارات الموجودة بالفعل ووضع السلوك المتوقع قبل أن يُعمل على المترجم نفسه لوضع الخاصية، فلنقل أن الإدخال لم يكن موجودا ونريد أن نعمل على الدالة `قراءة_عدد` في alifstandardlib.alif، هكذا ستكون هيكلية الملفات:

```
- <أكواد ألف>
    - اختبارات
        - أكواد
        - الإدخال
            - ادخل_رقما.ألف
            - ادخل_رقما_توقع.json
```

الملف `./اختبارات/أكواد/الإدخال/ادخل_رقما.ألف`

```
#ألف

دالة رئيسية
    عدد ع = قراءة_عدد()
    اطبع(ع)
نهاية دالة
```

الآن لنأخذ قالب التوقع من `./اختبارات/قالب_التوقع.yml`، الملف `./اختبارات/أكواد/الإدخال/ادخل_رقما_توقع.yml` سيكون بنفس محتوى القالب، إلا أننا سنغير خانة `تنفيذ.دخل` ونضع فيها رقم متبوعا بسطر جديد (حتى تتم قراءة الرقم)، ونجعل خانة `تنفيذ.خرج` هي القيمة المطبوعة، وهي نفس القيمة المدخلة متبوعة بسطر جديد.

> ملاحطة: شغلت الاختبارات بملف كود ألف فقط (بدون ملف التوقع) سيتم إنشاء ملف التوقع تلقائيا وملؤه بما يحدث عند الترجمة والتنفيذ

```
تجميع:
  خرج: ""
  خطأ: ""
  رمز_الخروج: 0

تنفيذ:
  - دخل:
      - "123"
    خرج:
      - "123

        "
    خطأ:
      - ""
    رمز_الخروج: 0
```
