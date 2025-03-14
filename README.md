# SE_lab_s1

# توضیحات دستورات گیت (Git)

## پوشه‌ی `.git` چیست؟ چه اطلاعاتی در آن ذخیره می‌شود؟ با چه دستوری ساخته می‌شود؟

پوشه‌ی `.git` یک دایرکتوری مخفی در داخل یک مخزن گیت (repository) است که تمامی اطلاعات مربوط به مدیریت نسخه‌ها را ذخیره می‌کند. این اطلاعات شامل تاریخچه‌ی تغییرات، شاخه‌ها (branches)، اطلاعات مربوط به commitها، تنظیمات مخزن و غیره است.

این پوشه با دستور زیر ساخته می‌شود:
```sh
 git init 
```
پس از اجرای این دستور در یک پوشه‌ی پروژه، گیت آن را به یک مخزن گیت تبدیل کرده و پوشه‌ی `.git` را درون آن ایجاد می‌کند.

## منظور از atomic بودن در `atomic commit` و `atomic pull-request` چیست؟

**atomic commit** به این معنی است که هر commit باید یک تغییر مشخص و مستقل را دربر داشته باشد که اگر در یک مرحله اجرا نشود، هیچ بخشی از آن ذخیره نشود. این ویژگی باعث می‌شود که تغییرات ناقص در مخزن ذخیره نشوند و در صورت بروز مشکل، امکان بازگشت به وضعیت پایدار قبلی وجود داشته باشد.

**atomic pull-request** نیز به این معناست که وقتی یک pull request انجام می‌شود، تمامی تغییرات به‌صورت یکجا اعمال شده و در صورت بروز خطا، تمامی تغییرات به حالت قبل بازمی‌گردند.

## تفاوت دستورهای `fetch` و `pull` و `merge` و `rebase` و `cherry-pick`

### `git fetch`
این دستور آخرین تغییرات را از مخزن راه دور دریافت می‌کند، اما تغییرات را روی مخزن محلی اعمال نمی‌کند. فقط اطلاعات جدید را دانلود کرده و امکان بررسی آن‌ها را می‌دهد.

### `git pull`
این دستور ترکیبی از `git fetch` و `git merge` است. ابتدا تغییرات جدید را دریافت کرده و سپس آن‌ها را با شاخه‌ی فعلی ادغام (merge) می‌کند.

### `git merge`
این دستور تغییرات یک شاخه را با شاخه‌ی فعلی ترکیب می‌کند. در صورت وجود تغییرات متناقض (conflict)، باید آن‌ها را به‌صورت دستی برطرف کرد.

### `git rebase`
این دستور تغییرات یک شاخه را روی یک شاخه‌ی دیگر بازپخش (reapply) می‌کند. به جای ایجاد یک commit جدید برای ادغام، تاریخچه تغییرات را بازنویسی می‌کند.

### `git cherry-pick`
این دستور برای انتخاب و اعمال یک commit خاص از یک شاخه‌ی دیگر استفاده می‌شود، بدون این که کل شاخه را ادغام کند.

## تفاوت دستورهای `reset` و `revert` و `restore` و `switch` و `checkout`

### `git reset`
این دستور تغییرات شاخه‌ی فعلی را به یک commit قبلی برمی‌گرداند. در حالت `--hard` تمامی تغییرات حذف می‌شوند و در حالت `--soft` تغییرات حفظ شده ولی commitها حذف می‌شوند.

### `git revert`
برخلاف `reset` که تاریخچه را تغییر می‌دهد، این دستور یک commit جدید ایجاد می‌کند که تغییرات یک commit قبلی را برعکس می‌کند.

### `git restore`
این دستور برای بازیابی فایل‌ها به نسخه‌ی قبلی آن‌ها در history استفاده می‌شود، بدون این که commitها تغییر کنند.

### `git switch`
این دستور برای تغییر شاخه‌ها استفاده می‌شود. در گیت نسخه‌های جدید، به جای `checkout` برای تغییر شاخه‌ها از `switch` استفاده می‌شود.

### `git checkout`
این دستور دو کاربرد اصلی دارد: تغییر شاخه‌ها و بازیابی نسخه‌ی قبلی یک فایل. در نسخه‌های جدید گیت، استفاده از `switch` برای تغییر شاخه‌ها و `restore` برای بازیابی فایل‌ها توصیه می‌شود.

## منظور از `stage` یا همان `index` چیست؟ دستور `stash` چه کاری را انجام می‌دهد؟

### `stage` یا `index`
 مفهوم`stage` (یا `index`) ناحیه‌ای موقتی در گیت است که تغییرات قبل از انجام commit در آن قرار می‌گیرند. زمانی که فایلی را با دستور `git add` اضافه می‌کنیم، این تغییرات به `stage` منتقل می‌شوند اما هنوز commit نشده‌اند. این ویژگی به ما امکان می‌دهد تا تغییرات موردنظر خود را انتخاب کرده و تنها آن‌ها را در commit ثبت کنیم.

### `git stash`
این دستور تغییرات فعلی را به‌صورت موقت ذخیره کرده و شاخه‌ی کاری را به آخرین commit بازمی‌گرداند. این قابلیت زمانی مفید است که بخواهیم بدون commit کردن تغییرات، به شاخه‌ی دیگری برویم یا به وضعیت قبلی بازگردیم.

```sh
git stash
```

برای بازگرداندن تغییرات ذخیره‌شده:
```sh
git stash pop
```

برای مشاهده‌ی لیست stashها:
```sh
git stash list
```