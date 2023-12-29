# SE_Profiling

ابتدا نرم افزار Yourkit را نصب کرده و افزونه آن را به Intellij Idea اضافه می‌کنیم. سپس برنامه ProfilingTest را به پروژه اضافه می‌کنیم و طبق دستور آزمایش فایل JavaCup را به واسطه افزونه موردنظر اجرا می‌کنیم:

<img width="602" alt="1" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/28235e8a-a447-454e-9ecf-115f68b9e8b9">

سه عدد بعنوان ورودی وارد میکنیم:

<img width="538" alt="3" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/759192e5-30bd-4947-9233-e4d2ef9dd815">


وقتی از Yourkit Profiler بخش Performance charts را بررسی کنیم متوجه میزان استفاده از CPU میشویم:

<img width="913" alt="2" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/cac9a0bd-5d10-4cae-b04f-2cfabf8f9cfd">

همچنین در بخش Memory نیز امکان بررسی وضعیت استفاده از حافظه وجود دارد:

<img width="604" alt="4" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/8d1f340a-253a-4c1d-aff6-d360fb6825db">

همانطور که مشخص است حافظه Heap رو به پر شدن است.

با استفاده از Method list نیز میتوان متوجه شد که بیشترین مصرف CPU اختصاص داده شده به تابع temp و Arraylist است:

<img width="921" alt="13" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/c6e97465-6a99-471f-af74-05c6e46e4010">

 این کلاس شامل دو حلقه است که دو ایندکس i و j را جمع می‌کنند و حاصل را در یک ArrayList قرار می‌دهند. برای حل این مشکل، می‌توان از Array به جای ArrayList استفاده کرد تا عملکرد کد بهبود یابد. بنابراین بصورت زیر تغییرات را اعمال میکنیم: 

 <img width="303" alt="5" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/04452fc4-f926-40c9-80f6-00ad0a6793fa">

سپس مجددا تخصیص منابع را مشابه مرحله قبل چک میکنیم:

<img width="922" alt="6" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/33482b23-febe-4483-b831-62e2bee774ae">

<img width="924" alt="7" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/dd1ce37c-4232-42a4-a059-155b28c840af">

همانطور که پیداست نتایج به میزان خوبی تغییر یافته و تخصیص منابع کاهش پیدا کرده است.

--------------------------------------------

بخش دوم

در این بخش یک کلاس با ماموریت محاسبه تابع فیبوناچی اضافه میکنیم که در ابتدا از روش بازگشتی استفاده می‌کند که می‌تواند به مصرف حافظه زیاد و زمان محاسبه طولانی برای اعداد بزرگتر از حد معقول منجر شود.

<img width="501" alt="14" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/693f3e17-842b-4e36-b11b-4bf1745186a0">

وضعیت تخصیص منابع:

<img width="924" alt="9" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/1cd7fb6b-010a-488f-b091-961027378fe7">

<img width="921" alt="10" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/a95d77f7-f9c4-4554-aaac-667ff85a7983">

برای کاهش استفاده از منابع و بهبود کد، مراحل زیر را طی می‌کنیم:

استفاده از حلقه به جای روش بازگشتی:
به جای استفاده از تابع بازگشتی برای محاسبه فیبوناچی، از یک حلقه استفاده کردیم که بهینه‌تر است.
```
for (int i = 2; i <= n; i++) {
    fibArray[i] = fibArray[i - 1] + fibArray[i - 2];
}
```

در کد اولیه از متغیرهای موقت برای ذخیره مقادیر محاسبه شده استفاده می‌شد، اما در کد بهینه‌تر از یک آرایه برای ذخیره مقادیر استفاده کردیم که منجر به کاهش مصرف حافظه می‌شود.

```
long[] fibArray = new long[n + 1];
```

شرط ابتدایی در تابع بازگشتی نیز حذف شده و به صورت جداگانه در تابع اصلی اعمال شده است.
```
if (n <= 1) {
    return n;
}
```

کد بهینه‌شده بصورت زیر خواهد بود:

<img width="607" alt="15" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/76a65667-6b06-4202-9a08-061bef77e835">


حال مجددا نتایج Profiling را مشاهده می‌کنیم:

<img width="925" alt="11" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/0fa5104f-98db-43a1-bb6f-18175849d577">

<img width="923" alt="12" src="https://github.com/epMahdiyeh/SE_Profiling/assets/62205305/67fdd5b5-9cef-4cfe-bc7b-8fc5eccc2bf6">

همانطور که پیداست میزان استفاده از منابع بطور چشمگیری کاهش پیدا کرده است.



 
