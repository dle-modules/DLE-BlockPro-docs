# Модификаторы данных в шаблоне

Модификаторы предназначены для изменения, выводимых через шаблон, данных.

!>Общая информация по использованию модификаторов находится в [разделе помощи к шаблонизатору](https://github.com/bzick/fenom/blob/master/docs/ru/readme.md#%D0%9C%D0%BE%D0%B4%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%82%D0%BE%D1%80%D1%8B).<br> Все модификаторы Fenom можно использовать в модуле.

На этой странице перечислены модификаторы, используемые в модуле BlockPro.

<!-- panels:start -->

<!-- div:title-panel -->
## limit

<!-- div:left-panel -->
Ограничение количества символов контента.

Принимает три параметра:

1. Максимальное количество символов в тексте.  
2. Текст, показываемый в конце обрезанной строки.
3. Жесткое ограничение символов. Если передать `true` не будет учитываться логический конц слова.

<!-- div:right-panel -->
```tpl
Вывести 150 символов:
{$el.short_story|limit:'150'}

Вывести 50 символов и троеточие в конце:
{$el.short_story|limit:'50':'&hellip;'}

Вывести 30 символов, троеточие в конце и жестко обрезать тест без учёта слов:
{$el.short_story|limit:'50':'&hellip;':true}
```



<!-- div:title-panel -->
## image

<!-- div:left-panel -->
Получение изображения из контента.

Так же можно использовать модификаторы **tinypng** и **kraken**

**image** — встроенный функционал.

**tinypng** — получение картинки через сервис [tinypng.com](https://tinypng.com/)

**kraken** — получение картинки через сервис [kraken.io](https://kraken.io/)

Принимает следующие параметры:

1.  **(string) \$data** — Строка, из которой будем брать картинку/картинки
2.  **(string) \$noimage** — Картинка-заглушка
3.  **(string) \$imageType** — Тип картинки (small/original/intext) - для получения соответствующей картинки или массива картинок
4.  **(integer/string) \$number** — Номер картинки в контенте или all для вывода всех картинок
5.  **(string) \$size** — Размер картики (например 100 или 100x150)
6.  **(string) \$quality** — Качество картинки (0-100)
7.  **(string) \$resizeType** — Тип ресайза (exact, portrait, landscape, auto, crop)
8.  **(boolean) \$grabRemote** — скачивать картинки со сторонних сайтов к себе (true/false)
9.  **(boolean) \$showSmall** — Обрабатывать уменьшенную копию, если есть
10. **(string) \$subdir** — Подпапка для картинок

<!-- div:right-panel -->
```tpl
{$el.short_story|image:$noimage:'small':'1':'':'':'':true:false:'/uploads/myfolder'}

{$el.full_story|image:$noimage:'intext':'all':'150x450':'':'landscape':true:false}

{$el.full_story|tinypng:$noimage:'small':'1':'150':'':'crop':true:false}

{$el.full_story|kraken:$noimage:'small':'1':'150':'':'crop':true:false}
```



<!-- div:title-panel -->
## declination

<!-- div:left-panel -->
Склонение слова в соответствии с количеством. 

Например: 1 коментарий, 2 комментария, 100 комментариев

<!-- div:right-panel -->
```tpl
Выведет текст: 15 комментариев
{$el.comm_num} {$el.comm_num|declination:'комментари|й|я|ев'} 
```



<!-- div:title-panel -->
## dateformat

<!-- div:left-panel -->
Форматирование даты в соответствии с маской.

Аналог `{date="D m Y"}`

<!-- div:right-panel -->
```tpl
{$el.date|dateformat}

{$el.date|dateformat:"d F Y"}
```



<!-- div:title-panel -->
## timeago

<!-- div:left-panel -->
Форматирование даты в формате "time ago".

В качестве параметра модификатор принимает цифру от 0 до 6, указывающую точность вывода от года до минут. По умолчанию установлено значение 2.

<!-- div:right-panel -->
```tpl
Выведет результат: 
2 года, 4 месяца, 1 неделю, 6 дней, 12 часов и 5 минут назад.
{$el.date|timeago:6}
```



<!-- div:title-panel -->
## catinfo

<!-- div:left-panel -->
Выводит информацию о категории или категориях, к которой принадлежит новость.
 
<!-- div:right-panel -->
```tpl
Весь массив данных: 
{$el.category|catinfo}

Название категории: 
{$el.category|catinfo:'name'}

Ссылка на категорию: 
{$el.category|catinfo:'link'}

URL категории: 
{$el.category|catinfo:'url'}

Иконка категории: 
{$el.category|catinfo:'icon'}

Иконка категории (с заглушкой): 
{$el.category|catinfo:'icon':$noimage}
```



<!-- div:title-panel -->
## getAuthors

<!-- div:left-panel -->
Получает информацию о пользователях, добавивших новости непосредственно в шаблоне.

Более детальную информацию о процедуре получения пользователей можно увидеть в шаблоне getuserinfo.tpl

<!-- div:right-panel -->
```tpl
{set $users = []}

{foreach $list as $el}
  {set $users[] = $el.autor}
{/foreach}

{set $arUsers = $users|getAuthors:'email, user_id, news_num, comm_num, foto'}

{unset $users}

<pre>{$arUsers|dump}</pre>
```



<!-- div:title-panel -->
## ematch\_all

<!-- div:left-panel -->
Модификатор **ematch\_all** является аналогом php-функции **preg\_match\_all**. 

Применяется к любой строке. 

В качестве параметра принимает регулярное выражение. 

Возвращает массив с найденными совпадениями или пустой массив.
<!-- div:right-panel -->
```tpl
{foreach $list as $key => $el}
  {set $totalGifs = 0}
  {set $otherImages = 0}
  {set $images = $el.short_story|ematch_all:'/<img(?:\\s[^<>]*?)?\\bsrc\\s*=\\s*(?|"([^"]*)"|\'([^\']*)\'|([^<>\'"\\s]*))[^<>]*>/i'}
 {if $images[1]|length}
   {foreach $images[1] as $image}
  {if ('dleimages' in $image) || ('engine/data/emoticons' in $image)}
   {continue}
   {/if}
   {set $imgInfo = $image|pathinfo}
     {if $imgInfo.extension == 'gif'}
       {set $totalGifs = $totalGifs + 1}
     {else}
       {set $otherImages = $otherImages + 1}
     {/if}
   {/foreach}
 {/if}

  <p>
    В новости <b><a href="{$el.url}">{$el.title}</a></b>
    {$totalGifs} {$totalGifs|declination:'гиф|ка|ки|ок'}, 
    а так же 
    {$otherImages} {$otherImages|declination:'|другая картинка|других картинки|других картинок'} 
  </p>

{/foreach}

```

<!-- div:title-panel -->
## sentence

<!-- div:left-panel -->
Выводит заданное количество предложений (до точки). 

Иногда полезно для вывода завершенных предложений, а не слов.
<!-- div:right-panel -->
```tpl
Выведет два первых предложения из краткой новости.:
<pre>{$el.short_story|sentence:'2'}</pre>

```

<!-- panels:end -->


<!-- div:title-panel -->
## dump

<!-- div:left-panel -->
Выводит данные через php-функцию **print\_r**. 

Крайне полезно для отладки во время разработки шаблона.
<!-- div:right-panel -->
```tpl
Выведет всё содержимое массива одной новости:
<pre>{$el|dump}</pre>

Выведет содержимое допполей как есть:
<pre>{$el.xfields|dump}</pre>

```

<!-- panels:end -->
