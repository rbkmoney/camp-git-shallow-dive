class: impact

# git
## the stupid content tracker

---

layout: true
title: Задачи
class: animation-fade

# {{title}}

---

## Контроль версий

--
Я работаю над сложным проектом с изменяющимися требованиями и далёким горизонтом развития.

--

Я хочу иметь возможность _версионировать_ мою работу.

---

### Откат к предыдущим состояниям
--

* Почему бы просто не взять флешку и скопировать в `Новая папка (2)`?
--
 😔

--
* Ну хорошо, что если я буду записывать в `Новая папка {Текущее время}`?
--
 😔

<pre class="terminal">
<span style="color:gray;">❯ git checkout OTP-21.0.3</span>
Checking out files: 100% (3448/3448), done.
Note: checking out 'OTP-21.0.3'.
</pre>

---

### Быстрое восстановление работоспособности
--

* Ведь я могу просто скинуть с флешки последнюю `Новую папку`, что не так?
--
 😔

<pre class="terminal">
<span style="color:gray;">❯ git reset --hard HEAD</span>
</pre>

<pre class="terminal">
HEAD is now at a3a900e382 Updated OTP version
</pre>

---

### Внесение осмысленных изменений
--

* Я могу просто положить рядом файл с названием `Зачем.txt`, почему нет? 
--
 😔

<pre class="terminal">
<span style="color:gray;">❯ git commit -a</span>
</pre>

<pre class="terminal">
Outline installation flow

<span style="color:gray;"># Please enter the commit message for your changes. Lines starting</span>
<span style="color:gray;"># with '#' will be ignored, and an empty message aborts the commit.</span>
<span style="color:gray;">#</span>
<span style="color:gray;"># On branch v0</span>
<span style="color:gray;"># Your branch is up to date with 'origin/v0'.</span>
<span style="color:gray;">#</span>
<span style="color:gray;"># Changes to be committed:</span>
<span style="color:gray;">#       modified:   README.md    </span>
</pre>

---

### Отслеживание изменений
--

* Важен не процесс, а результат.
--
 🤔

<pre class="terminal">
<span style="color:yellow;">commit f918ca5f58f52d028b7ea140b874f8a79395ae65</span>
Author: Andrew Mayorov &lt;encube.ul@gmail.com&gt;
Date:   Wed Jul 18 17:49:27 2018 +0300

    Downgrade to rbkmoney/hellgate@79e70142 (#981)

<span style="font-weight:bold;">diff --git a/pillar/wetkitty/macroservice.sls b/pillar/wetkitty/macroservice.sls</span>
<span style="font-weight:bold;">index 7234ee0..04e2ad2 100644</span>
<span style="font-weight:bold;">--- a/pillar/wetkitty/macroservice.sls</span>
<span style="font-weight:bold;">+++ b/pillar/wetkitty/macroservice.sls</span>
<span style="color:aqua;">@@ -49,7 +49,7 @@</span> wetkitty:
 
     hellgate:
       image-name: &quot;dr.rbkmoney.com/rbkmoney/hellgate&quot;
<span style="color:red;">-      image-tag:  &quot;1ae0c4b1f3e1e4325eed5618c56bedcb823cf0e8&quot;</span>
<span style="color:lime;">+</span><span style="color:lime;">      image-tag:  &quot;79e70142161cc5a9a995dc77601fc72514cb19f9&quot;</span>
       memory-limit: 256M
       service-name: &quot;hellgate&quot;
</pre>

---

layout: true
title: Задачи
class: animation-fade

# {{title}}

---

## Совместная работа

--
Я больше не работаю над этим проектом один, _нас_ много.

--

У каждого из нас есть _имя_, и я знаю кто есть кто.

--

Я должен уметь работать и вносить изменения, не мешая без необходимости моим коллегам.

--

Мы должны иметь возможность обмениваться результатами работы друг с другом.

---

### Авторство
--

* Моя файловая система проследит за этим. Или нет?
--
 😔

<pre class="terminal">
<span style="color:gray;">❯ git config --global</span> user.name <span style="color:yellow;">Keynfawkes</span>
</pre>

<pre class="terminal">
<span style="color:gray;">❯ git config --global</span> user.email <span style="color:yellow;">a.mayorov@rbkmoney.com</span>
</pre>

---

### Независимая разработка
--

* Это просто, нужно всего лишь давать уникальный префикс папкам на флешке.
--
 😫

<pre class="terminal">
<span style="color:gray;">❯ git checkout -b ft/proper-transfers</span>
</pre>

<pre class="terminal">
<span style="color:gray;">❯ git status</span>
On branch ft/proper-transfers
Your branch is up to date with 'rbkmoney/ft/proper-transfers'.

Untracked files:
  (use &quot;git add &lt;file&gt;...&quot; to include in what will be committed)

    <span style="color:red;">THOUGHTS.md</span>

nothing added to commit but untracked files present (use &quot;git add&quot; to track)
</pre>

---

### Разрешение конфликтов
--

* Я просто перезапишу чужие изменения.
--
 😡

<pre class="terminal">
<span style="font-weight:bold;">diff --cc pillar/wetkitty/macroservice.sls</span>
<span style="font-weight:bold;">index a13392b,432a332..0000000</span>
<span style="font-weight:bold;">--- a/pillar/wetkitty/macroservice.sls</span>
<span style="font-weight:bold;">+++ b/pillar/wetkitty/macroservice.sls</span>
<span style="color:aqua;">@@@ -281,23 -191,15 +291,31 @@@</span>
  
      proxy-mocketbank:
        image-name: &quot;dr.rbkmoney.com/rbkmoney/proxy-mocketbank&quot;
<span style="color:lime;">++&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD</span>
<span style="color:lime;"> +      image-tag:  &quot;fbd79a2a9a100adef9b5c4e67842e2e86d914249&quot;</span>
<span style="color:lime;">++=======</span>
<span style="color:lime;">+       image-tag:  &quot;5e5646e90d4eec15c8bae36af9281230a33cce20&quot;</span>
<span style="color:lime;">++&gt;&gt;&gt;&gt;&gt;&gt;&gt; origin/ft/PROX-90/woody</span>
        memory-limit: 512M
        service-name: &quot;proxy-mocketbank&quot;
        java:
          xmx: 256m
      
</pre>

---

### Аудит изменений
--

* Я просто спрошу своих коллег, каждого по очереди.
--
 😡

<pre class="terminal">
<span style="color:gray;">❯ git blame --date=relative -L100,112 pillar/wetkitty/macroservice.sls</span>
</pre>

<pre class="terminal">
d8485b5e (niku64      1 year 7 months ago  101)  capi:
8899c7ab (A. Belyaev  9 months ago         102)    v1:
8899c7ab (A. Belyaev  9 months ago         103)      image-name: &quot;dr.rbkmoney.com/rbkmoney/capi-v1&quot;
b985f601 (E. Levenets 2 weeks ago          104)      image-tag:  &quot;3302c4abc25e4805122d119ebd7b2f6fc1f706a3&quot;
8899c7ab (A. Belyaev  9 months ago         105)      memory-limit: 512M
8899c7ab (A. Belyaev  9 months ago         106)      service-name: &quot;capi-v1&quot;
8899c7ab (A. Belyaev  9 months ago         107)    v2:
8899c7ab (A. Belyaev  9 months ago         108)      image-name: &quot;dr.rbkmoney.com/rbkmoney/capi-v2&quot;
b985f601 (E. Levenets 2 weeks ago          109)      image-tag:  &quot;29d1418564405f6789356a0929c33668e4fdf23a&quot;
8899c7ab (A. Belyaev  9 months ago         110)      memory-limit: 512M
8899c7ab (A. Belyaev  9 months ago         111)      service-name: &quot;capi-v2&quot;
</pre>

---

layout: true
title: Модель
class: animation-fade

# {{title}}

---

## Приоритеты
--

* Скорость работы

--

* Простота внутреннего устройства

--

* Поддержка разработки с сотнями одновременно изменяемых веток

--

* Распределённость

--

* Умение управляться с проектами **огромных** размеров

---

## Технические решения
--

* Состояние вместо набора изменений

--

* Локальная копия **всех** внесённых в процессе разработки изменений

--

* Контрольные хэши в качестве идентификаторов **любых** изменений

--

* История измнений не подлежит удалению или манипуляции

---

## Репозиторий
--

<pre class="terminal">
<span style="color:gray;">❯ ls -la .git</span>
</pre>

<pre class="terminal">
drwxr-xr-x   14 keynslug  staff    448 Jul 23 19:44 <span style="font-weight:bold;"></span><span style="color:aqua;font-weight:bold;">.</span><span style="color:white;background-color:white;font-weight:bold;"></span>
drwxr-xr-x   25 keynslug  staff    800 Jun 20 14:25 <span style="font-weight:bold;"></span><span style="color:aqua;font-weight:bold;">..</span><span style="color:white;background-color:white;font-weight:bold;"></span>
-rw-r--r--    1 keynslug  staff   2769 Jul 23 19:44 COMMIT_EDITMSG
-rw-r--r--    1 keynslug  staff   1167 Jul 16 17:37 FETCH_HEAD
-rw-r--r--    1 keynslug  staff     19 Jul 16 17:37 HEAD
-rw-r--r--    1 keynslug  staff     41 Jul 16 17:37 ORIG_HEAD
-rw-r--r--    1 keynslug  staff   1614 Jul 15 19:07 config
-rw-r--r--    1 keynslug  staff     73 Apr  5 15:24 description
drwxr-xr-x   13 keynslug  staff    416 Apr  5 15:24 <span style="font-weight:bold;"></span><span style="color:aqua;font-weight:bold;">hooks</span><span style="color:white;background-color:white;font-weight:bold;"></span>
-rw-r--r--    1 keynslug  staff  13103 Jul 16 17:37 index
drwxr-xr-x    3 keynslug  staff     96 Apr  5 15:24 <span style="font-weight:bold;"></span><span style="color:aqua;font-weight:bold;">info</span><span style="color:white;background-color:white;font-weight:bold;"></span>
drwxr-xr-x    4 keynslug  staff    128 Apr 10 19:47 <span style="font-weight:bold;"></span><span style="color:aqua;font-weight:bold;">logs</span><span style="color:white;background-color:white;font-weight:bold;"></span>
drwxr-xr-x  254 keynslug  staff   8128 Jul 12 15:30 <span style="font-weight:bold;"></span><span style="color:aqua;font-weight:bold;">objects</span><span style="color:white;background-color:white;font-weight:bold;"></span>
drwxr-xr-x    6 keynslug  staff    192 Jun 13 11:22 <span style="font-weight:bold;"></span><span style="color:aqua;font-weight:bold;">refs</span><span style="color:white;background-color:white;font-weight:bold;"></span>
</pre>

---

## Коммиты
--

* Фрагмент истории проекта

<pre class="terminal">
<span style="color:yellow;">commit 879046011d1dbb845537628cc61eaae98dcf8c9c</span>
Parent: 0a8b2bf3a13593bdd70e46cc0b4cce5e714cb285
Author: Andrew Mayorov &lt;encube.ul@gmail.com&gt;
Date:   Sun Jul 15 19:10:33 2018 +0300

    CAPI-262: Make `bin` example look in line w/ definition (#26)

 api/payres/spec/definitions/SecuredBankCard.yaml | 2 <span style="color:lime;">+</span><span style="color:red;">-</span>
 1 file changed, 1 insertion(+), 1 deletion(-)
</pre>

--

* Осмысленная единица изменения

--
    - **Зачем?** Сообщение
--
    - **Кто?** Автор
--
    - **Когда?** Время
--
    - **Что?** Набор изменённых файлов
--
    - **Где?** Хэш, хэш родительского коммита

---

## Ветки
--

* Пространство для манёвров

--

* Название для определённой осмысленной истории изменений

--

* Набор **коммитов**, наложенных на **базовую** ветку

---

## Ветки
--

<pre class="terminal">
<span style="color:gray;">❯ git checkout -b</span> fix/spelling
</pre>
<pre class="terminal">
Switched to a new branch 'fix/spelling'
</pre>

--

<pre class="terminal">
<span style="color:gray;">❯ git log --oneline</span> HEAD~3..
</pre>
<pre class="terminal">
<span style="color:yellow;">8790460</span><span style="color:yellow;"> (</span><span style="color:aqua;font-weight:bold;">HEAD -&gt; </span><span style="color:lime;font-weight:bold;">fix/spelling</span><span style="color:yellow;">, </span><span style="color:red;font-weight:bold;">origin/master</span><span style="color:yellow;">, </span></span><span style="color:lime;font-weight:bold;">master</span><span style="color:yellow;">)</span> CAPI-262: Make `bin` example look in line w/ definition (#26)
<span style="color:yellow;">0a8b2bf</span> CAPI-262: Stash deposits for later (#21)
<span style="color:yellow;">04db123</span> CAPI-262: Stash identity challenge cancellation (#23)
</pre>

--

<pre class="terminal">
<span style="color:gray;">❯ cat</span> .git/refs/heads/fix/spelling .git/refs/heads/master                                                                                     fix/spelling
</pre>
<pre class="terminal">
879046011d1dbb845537628cc61eaae98dcf8c9c
879046011d1dbb845537628cc61eaae98dcf8c9c
</pre>

---

## Состояния файлов
--

* Находящиеся в **стейджинге**, попадающие в грядущий коммит
<pre class="terminal">
Changes to be committed:
  (use &quot;git reset HEAD &lt;file&gt;...&quot; to unstage)

    <span style="color:lime;">new file:   README.md</span>
</pre>

---

## Состояния файлов

* Изменённые в **рабочей копии** репозитория, но ещё не попавшие в **стейджинг**
<pre class="terminal">
Changes not staged for commit:
  (use &quot;git add &lt;file&gt;...&quot; to update what will be committed)
  (use &quot;git checkout -- &lt;file&gt;...&quot; to discard changes in working directory)

    <span style="color:red;">modified:   SCENARIOS.md</span>
</pre>

---

## Состояния файлов

* Новые, ещё не включённые в **репозиторий**
<pre class="terminal">
Untracked files:
  (use &quot;git add &lt;file&gt;...&quot; to include in what will be committed)

    <span style="color:red;">package-lock.json</span>
    <span style="color:red;">withdrawal.svg</span>
    <span style="color:red;">withdrawal.wsd</span>
</pre>

---

## Объекты

* Каждый элемент репозитория – **объект**

--

    - файл
--

    - директория
--

    - коммит

---

## Объекты

* Сделаем новый коммит на ветку v0

<pre class="terminal">
<span style="color:gray;">❯ git commit -m</span> 'Add more TODOs'
</pre>

<pre class="terminal">
[v0 6b6061d] Add more TODOs
 1 file changed, 12 insertions(+), 4 deletions(-)
</pre>

---

## Объекты

* Посмотрим, что получилось

<pre class="terminal">
<span style="color:gray;">❯ git show --stat</span> v0
</pre>

<pre class="terminal">
<span style="color:yellow;">commit 6b6061d9dadd271f9c68d11df90f3c63711dbf8b</span>
Author: Andrey Mayorov &lt;a.mayorov@rbkmoney.com&gt;
Date:   Mon Jul 23 20:32:25 2018 +0300

    Add more TODOs

 README.md | 16 <span style="color:lime;">++++++++++++</span><span style="color:red;">----</span>
 1 file changed, 12 insertions(+), 4 deletions(-)
</pre>

---

## Объекты

* Посмотрим, какое теперь состояние ветки v0

<pre class="terminal">
<span style="color:gray;">❯ cat</span> .git/refs/heads/v0
</pre>

<pre class="terminal">
6b6061d9dadd271f9c68d11df90f3c63711dbf8b
</pre>

---

## Объекты

* Прочитаем, _что_ записано в commit object

<pre class="terminal">
<span style="color:gray;">❯ git cat-file -p 6b6061d9dadd271f9c68d11df90f3c63711dbf8b</span>
</pre>

<pre class="terminal">
tree 6fda390e9a9b9a6c92a89fdfa49ffa21d7aede64
parent 879046011d1dbb845537628cc61eaae98dcf8c9c
author Andrey Mayorov <a.mayorov@rbkmoney.com> 1532367145 +0300
committer Andrey Mayorov <a.mayorov@rbkmoney.com> 1532367145 +0300

Add more TODOs
</pre>

--

* Абсолютно у каждого коммита есть **родительский** коммит

---

## Объекты

* Посмотрим на состояние tree object

<pre class="terminal">
<span style="color:gray;">❯ git cat-file -p</span> 6fda390e9a9b9a6c92a89fdfa49ffa21d7aede64
</pre>

<pre class="terminal">
100644 blob cddabd62522ad78c23e476a2610eccb048799d83    .gitignore
100644 blob 007daaf6d80329761f298635dfc8178cd6454ed5    Makefile
100644 blob cd87e33b43be29610317197890c0d2b4b607c2f1    README.md
040000 tree 661a6471b416f080efa1d3e51bef0c95028e2ab7    api
100644 blob 133f3456a4e424d1c625786fc746b7b48ee1f496    gulpfile.js
100644 blob 226cd9fdceff689a97af269634065e6ce655a8d1    package.json
040000 tree 857588a242ee82881aa19736b02e14c178ac4435    scripts
040000 tree af474cb37b5668fd23f8590aac3bd9b569dc8b2f    spec
040000 tree a6dcc3e3db0213af966837d671f077128dedba30    web
100644 blob 2ab2153d2eb0261252c21ed65e8186974917a2a7    wercker.yml
</pre>

--

* На самом деле изменился только хэш blob object, соответствующего `README.md`

---

## Объекты

* Посмотрим, как теперь выглядит blob object, соответствующий `README.md`

<pre class="terminal">
❯ git cat-file -p cd87e33b43be29610317197890c0d2b4b607c2f1                                                                                                   v0
</pre>

<pre class="terminal">
# Wallet API Specification

## TODO

* Надо бы ввести identity service terms.
...
</pre>

---

## Слияния

* Процесс внесения изменений разных авторов в **основную** ветку

---

## Слияния

<pre class="terminal">
<span style="color:gray;">❯ git merge stash/deposits</span>
</pre>

--

<pre class="terminal">
Merge branch 'stash/deposits' into v0

<span style="color:gray;"># Please enter a commit message to explain why this merge is necessary,</span>
<span style="color:gray;"># especially if it merges an updated upstream into a topic branch.</span>
<span style="color:gray;">#</span>
<span style="color:gray;"># Lines starting with '#' will be ignored, and an empty message aborts</span>
<span style="color:gray;"># the commit.</span>
</pre>

--

<pre class="terminal">
Merge made by the 'recursive' strategy.
 api/wallet/spec/definitions/BankCardPaymentResource.yaml         |  4 <span style="color:lime;">++++</span>
 api/wallet/spec/definitions/BankWirePaymentResource.yaml         |  3 <span style="color:lime;">+++</span>
 api/wallet/spec/definitions/Deposit.yaml                         | 34 <span style="color:lime;">++++++++++++++++++++++++++++++++++</span>
 api/wallet/spec/definitions/DepositEvent.yaml                    | 21 <span style="color:lime;">+++++++++++++++++++++</span>
 api/wallet/spec/definitions/DepositEventChange.yaml              | 12 <span style="color:lime;">++++++++++++</span>
 api/wallet/spec/paths/deposits.yaml                              | 29 <span style="color:lime;">+++++++++++++++++++++++++++++</span>
 api/wallet/spec/paths/deposits@{depositID}.yaml                  | 17 <span style="color:lime;">+++++++++++++++++</span>
 api/wallet/spec/paths/deposits@{depositID}@events.yaml           | 21 <span style="color:lime;">+++++++++++++++++++++</span>
 api/wallet/spec/swagger.yaml                                     | 13 <span style="color:lime;">+++++++++++++</span>
 15 files changed, 227 insertions(+)
</pre>

---

## Слияния

* Посмотрим, как выглядит commit object

<pre class="terminal">
<span style="color:gray;">❯ git cat-file -p</span> 9453ded6dfa17c21d2e10c9c2a2464d3ea24e1f3                                                                                                   v0
</pre>

<pre class="terminal">
tree 1baafb778c172fc3d2b3481ccd968dd93452d61f
parent 6b6061d9dadd271f9c68d11df90f3c63711dbf8b
parent 1b232523c7a6714ca8b624d79107987947c1c985
author Andrey Mayorov &lt;a.mayorov@rbkmoney.com&gt; 1532369793 +0300
committer Andrey Mayorov &lt;a.mayorov@rbkmoney.com&gt; 1532369793 +0300

Merge branch 'stash/deposits' into v0
</pre>

--

* Commit object с **двумя** родительскими коммитами

---

## Слияния

* Посмотрим, как выглядит история

<pre class="terminal">
<span style="color:gray;">git log --oneline --graph</span> HEAD~8..
</pre>

<pre class="terminal">
*   <span style="color:yellow;">a183297</span> Merge branch 'stash/deposits' into v0
<span style="color:red;">|</span><span style="color:lime;">\</span>  
<span style="color:red;">|</span> * <span style="color:yellow;">1b23252</span> Revert &quot;CAPI-262: Stash deposits for later (#21)&quot;
* <span style="color:lime;">|</span> <span style="color:yellow;">6b6061d</span> Add more TODOs
* <span style="color:lime;">|</span> <span style="color:yellow;">8790460</span> CAPI-262: Make `bin` example look in line w/ definition (#26)
<span style="color:lime;">|</span><span style="color:lime;">/</span>  
* <span style="color:yellow;">0a8b2bf</span> CAPI-262: Stash deposits for later (#21)
* <span style="color:yellow;">04db123</span> CAPI-262: Stash identity challenge cancellation (#23)
* <span style="color:yellow;">e004ee2</span> CAPI-262: Fix a couple of unusedness warnings (#22)
* <span style="color:yellow;">d3d07cc</span> CAPI-262: Fix residence param length (#20)
* <span style="color:yellow;">cdfe496</span> CAPI-262: Fix case sensitivity in query params too (#18)
</pre>

--

* Две независимо разрабатываемые ветки успешно слились в одну

---

## Удалённые репозитории
--

* Для синхронизации с коллегами необходимо доставлять свои изменения в удалённый репозиторий

--

* Чтобы прогрессировать в работе над единым проектом, нужно выбрать схему работы (workflow)

--
    - Централизованный репозиторий, свободно принимающий любые изменения

--
    - Интеграционный репозиторий, принимающий запросы на включение изменений (pull requests) из форков (forks)
--
 👍

---

## Удалённые репозитории

* Склонируем интеграционный репозиторий с проектом

<pre class="terminal">
<span style="color:gray;">❯ git clone</span> https://github.com/rbkmoney/camp-git-shallow-dive
</pre>
<pre class="terminal">
Cloning into 'swag-wallets'...
remote: Counting objects: 426, done.
remote: Compressing objects: 100% (78/78), done.
remote: Total 426 (delta 58), reused 110 (delta 40), pack-reused 288
Receiving objects: 100% (426/426), 126.16 KiB | 942.00 KiB/s, done.
Resolving deltas: 100% (170/170), done.
</pre>

--

* Узнаем, на какие удалённые репозитории он _ссылается_

<pre class="terminal">
<span style="color:gray;">❯ git remote -v</span>
</pre>
<pre class="terminal">
origin  https://github.com/rbkmoney/camp-git-shallow-dive (fetch)
origin  https://github.com/rbkmoney/camp-git-shallow-dive (push)
</pre>

---

## Удалённые репозитории

* Сделаем свой личный форк

<pre class="terminal">
<span style="color:gray;">❯ hub fork</span> keynslug
</pre>
<pre class="terminal">
Updating keynslug
From ssh://github.com/rbkmoney/camp-git-shallow-dive
 * [new branch]      master     -> keynslug/master
new remote: keynslug
</pre>

--

* Узнаем, на какие удалённые репозитории он теперь _ссылается_

<pre class="terminal">
<span style="color:gray;">❯ git remote -v</span>
</pre>
<pre class="terminal">
keynslug    git@github.com:keynslug/camp-git-shallow-dive.git (fetch)
keynslug    git@github.com:keynslug/camp-git-shallow-dive.git (push)
origin  https://github.com/rbkmoney/camp-git-shallow-dive (fetch)
origin  https://github.com/rbkmoney/camp-git-shallow-dive (push)
</pre>

---

## Удалённые репозитории

* Основное состояние проекта находится в ветке `master`

--

* Пора создать ветку для новых изменений

<pre class="terminal">
❯ git checkout -b ft/last-slides
</pre>
<pre class="terminal">
Switched to a new branch 'ft/last-slides'
</pre>

--

* И создать на ней коммит с необходимыми измнениями

<pre class="terminal">
❯ git add presentation.md
❯ git commit -m 'Add most presentation slides'
</pre>
<pre class="terminal">
[ft/last-slides 268c683] Add most presentation slides
 1 file changed, 701 insertions(+)
 create mode 100644 presentation.md
</pre>

---

## Удалённые репозитории

* Часто бывает так, что пока мы занимались этими изменениями, кто-то внёс изменения в основную ветку

--

* Нужно стараться синхронизировать _удалённые_ изменения

--

    В этот раз нам повезло

    <pre class="terminal">
    ❯ git fetch origin
    ❯ git merge origin/master
    </pre>
    <pre class="terminal">
    Already up to date.
    </pre>

---

## Удалённые репозитории

* Пора синхронизировать _наши_ изменения с нашим удалённым репозиторием

--

    <pre class="terminal">
    ❯ git push -u keynslug ft/last-slides
    </pre>
    <pre class="terminal">
    Counting objects: 3, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 6.68 KiB | 6.68 MiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To github.com:keynslug/camp-git-shallow-dive.git
     * [new branch]      ft/last-slides -> ft/last-slides
    Branch 'ft/last-slides' set up to track remote branch 'ft/last-slides' from 'keynslug'.
    </pre>

--

* Мы отправили **3** объекта, несложно понять, что это: сам commit, tree object и blob object с файлом `presentation.md`

--

* Теперь мы **отслеживаем** изменения в удалённой ветке `ft/last-slides`

---

## Удалённые репозитории

* Пора _интегрировать_ внесённые изменения в интеграционный репозиторий

--

* Создадим запрос на включение наших изменений

    <pre class="terminal">
    <span style="color:gray;">❯ hub pull-request</span>
    </pre>
    <pre class="terminal">
    Add the most of presentation slides

    <span style="color:gray;"># Requesting a pull to rbkmoney:master from keynslug:ft/last-slides</span>
    <span style="color:gray;">#</span>
    <span style="color:gray;"># Write a message for this pull request. The first block</span>
    <span style="color:gray;"># of text is the title and the rest is the description.</span>
    </pre>
    <pre class="terminal">
    https://github.com/rbkmoney/camp-git-shallow-dive/pull/1
    </pre>

--

* Мы запросили включение в основную ветку интеграционного репозитория (`rbkmoney:master`)

---

## Удалённые репозитории

* Дождёмся _одобрения_ нашего запроса

--

* После чего _интегратор_ произведёт включение, в результате которого произойдёт _слияние_ наших изменений с основной веткой

--

* Теперь нам необходимо синхронизировать состояние основной ветки с нашим локальным репозиторием
--
    <pre class="terminal">
    <span style="color:gray;">❯ git checkout</span> master
    </pre>
    <pre class="terminal">
    Switched to branch 'master'
    Your branch is up to date with 'origin/master'.
    </pre>

* Синхронизация ещё не проведена, локальный репозиторий не знает о произошедших изменениях

---

## Удалённые репозитории

* Получаем изменения с удалённого репозитория

    <pre class="terminal">
    <span style="color:gray;">❯ git pull</span> origin master
    </pre>
    <pre class="terminal">
    remote: Counting objects: 1, done.
    remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (1/1), done.
    From github.com:rbkmoney/camp-git-shallow-dive
       d4da560..43fe41a  master     -> origin/master
    </pre>

--

* Наблюдеам в истории появления коммита, фиксирующиего слияние наших изменений

    <pre class="terminal">
    <span style="color:gray;">❯ git log --oneline</span> keynslug/master..
    </pre>
    <pre class="terminal">
    <span style="color:yellow;">43fe41a</span><span style="color:yellow;"> (</span><span style="color:red;font-weight:bold;">origin/master</span><span style="color:yellow;">, </span><span style="color:lime;font-weight:bold;">master</span><span style="color:yellow;">)</span> Merge pull request #1 from keynslug/ft/last-slides
    <span style="color:yellow;">268c683</span><span style="color:yellow;"> (</span><span style="color:red;font-weight:bold;">keynslug/ft/last-slides</span><span style="color:yellow;">)</span> Add most presentation slides
    </pre>

---

class: impact animation-fade
layout: true

---

# Конец
## Надеюсь, хоть кто-то узнал что-то новое
