# Переменные строки подключения

!> **Внимание!** <br>В строке подключения модуля нет обязательных переменных, но у всех переменных есть значение по умолчанию.

Простейшая строка подключения модуля:

```smarty
{include file="engine/modules/base/blockpro.php"}
```

Переменные строки подключения указываются в виде конструкции: &param=value

?> Лучший способ составить строку подключения -- воспользоваться встроенным генератором строк, он учитывает особенности текущего сайта (например список категорий) и не даст ошибиться с пераметрами при составлении строки подключения.

<!-- panels:start -->

<!-- div:title-panel -->
## template
<!-- div:left-panel -->
Имя шаблона блока без расширения.

По умолчанию шаблон блока берётся из папки blockpro текущего шаблона сайта.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
&template=blockpro/blockpro
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?template=blockpro/custom}

{include file="engine/modules/base/blockpro.php?template=mytemplate}
```

<!-- div:title-panel -->
## moderate
<!-- div:left-panel -->
Если переменная указана - выводятся только новости на модерации.
<!-- div:right-panel -->

Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?moderate=y}
```

<!-- div:title-panel -->
## cachePrefix

<!-- div:left-panel -->
Дефолтный префикс кеша, нужен для автоматической чистки кеша при добавлении на сайте комментария или новости.

Автоматически удаляется, если задано время жизни кеша.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
&cachePrefix=news
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?cachePrefix=pref}
```

<!-- div:title-panel -->
## cacheSuffixOff
<!-- div:left-panel -->
Отключение суффикса кеша (будет создаваться один кеш-файл для всех пользователей).

По умолчанию для каждой группы пользователей создаётся свой кеш (на случай разного отображения контента разным юзерам). 

Если для всех групп пользователей контент одинаков - можно отключить.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?&cacheSuffixOff=y}
```

<!-- div:title-panel -->
## cacheNameAddon

<!-- div:left-panel -->

Служебная переменная. 

Назначает дополнение к имени кеша, если имеются переменные со значениями **this**, они будут автоматически дописаны в эту переменную, иначе для разных мест будет создаваться один и тот же файл кеша.

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?cacheNameAddon=newName}
```


<!-- div:title-panel -->
## nocache

<!-- div:left-panel -->
Отключает кеширование блока

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?&nocache=y}
```



<!-- div:title-panel -->
## cacheLive

<!-- div:left-panel -->
Задаёт время жизни кеша в минутах.

?> Этот параметр работает только при использовании файлового кеша"

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?cacheLive=15}
```



<!-- div:title-panel -->
## cacheVars

<!-- div:left-panel -->
Значимые параметры для формирования кеша. 

В переменную можно передавать через запятую ключи, доступные через `$_REQUEST` или значения переменной `$dle_module`

Эта функция полезна, если требуется выводить разное оформление в блоке с новостями для разных страниц сайта. 

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?caceVars=newsid,category,forum}
```
_В используемом примере будет создаваться отдельный кеш для каждой новости, для каждой категории и для модуля forum (при интеграции форума)._



<!-- div:title-panel -->
## startFrom

<!-- div:left-panel -->
С какой новости начать вывод (ноль - это первая новость, 3 - четвёртая)

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
&startFrom=0
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?startFrom=15}
```



<!-- div:title-panel -->
## limit

<!-- div:left-panel -->
Количество новостей в блоке

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
&limit=10
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?limit=20}
```



<!-- div:title-panel -->
## fixed

<!-- div:left-panel -->
Обработка фиксированных новостей:

- **yes** — показ всех (по умолчанию), фиксированные выше остальных;
- **only** — показ только фиксированных;
- **without** — показ только нефиксированных;
- **ignore** — показ единым списком без учёта признака фиксированных новостей;

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
&fixed=yes
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?fixed=only}
{include file="engine/modules/base/blockpro.php?fixed=witout}
{include file="engine/modules/base/blockpro.php?аixed=ignore}
```



<!-- div:title-panel -->
## postId
 
<!-- div:left-panel -->

ID новостей для вывода в блоке (через запятую, тире). 

Если указать **this** - будет взят ID просматриваемой новости. 

Может понадобиться для установки кастомизированных метатегов (актуально для киносайтов). 
При этом будет создаваться отдельный файл кеша для каждой просмотренной новости. Через тире указывается диапазон значений (от-до).

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?postId=1,5,23}
{include file="engine/modules/base/blockpro.php?postId=this}
{include file="engine/modules/base/blockpro.php?postId=1-10,15-30}
```



<!-- div:title-panel -->
## notPostId

<!-- div:left-panel -->
 
ID **игнорируемых** новостей (через запятую, тире). 

Если указать **this** - будет игнорироваться текущая новость, полезно например для вывода топа из текущей категории, но без текущей новости. 

При этом будет создаваться отдельный файл кеша для каждой просмотренной новости. 
Через тире указывается диапазон значений (от-до).

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?notPostId=10,50,55}
{include file="engine/modules/base/blockpro.php?notPostId=this}
{include file="engine/modules/base/blockpro.php?notPostId=1-15,55-90}
```



<!-- div:title-panel -->
## author

<!-- div:left-panel -->
 
Логины авторов, для показа их новостей в блоке (через запятую). 

Если указать **this** - будут браться новости автора из просматриваемого профиля, при этом будет создаваться отдельный файл кеша для каждой страницы профиля
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?author=admin,bot}
{include file="engine/modules/base/blockpro.php?author=this}
```



<!-- div:title-panel -->
## notAuthor

<!-- div:left-panel -->
 
Логины игнорируемых авторов (через запятую). 

Если указать **this** - будут игнорироваться новости автора из просматриваемого профиля, при этом будет создаваться отдельный файл кеша для каждой страницы профиля.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?notAuthor=bot}
{include file="engine/modules/base/blockpro.php?notAuthor=this}
```



<!-- div:title-panel -->
## xfilter

<!-- div:left-panel -->
 
Имена дополнительных полей для фильтрации по ним новостей (через запятую). 

Проверяется только заполненность поля. 

Если указать **this** - будут выводиться новости, в которых заполнено допполе, на странице которого находится пользователь, при этом будет создаваться отдельный файл кеша для каждой страницы допполя.

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?xfilter=image,text}
{include file="engine/modules/base/blockpro.php?xfilter=this}
```



<!-- div:title-panel -->
## notXfilter

<!-- div:left-panel -->
 
Имена дополнительных полей для игнорирования показа (через запятую). 

Проверяется только заполненность поля. 

Если указать **this** - будут ирнорироваться новости, в которых заполнено допполе, на странице которого находится пользователь, при этом будет создаваться отдельный файл кеша для каждой страницы допполя.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?notXfilter=image,text}
{include file="engine/modules/base/blockpro.php?notXfilter=this}
```




<!-- div:title-panel -->
## xfSearch

<!-- div:left-panel -->
 
Имена и значения допполей для фильтрации новостей по допполям с указанными значениями.

**Синтаксис передачи данных:** `&xfSearch=имя_поля|значение||имя_поля|значение`

?> Включение экспериментальных функций модуля повышает производительность  при использовании этого параметра.

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?xfSearch=name|value||name1|value1}
```




<!-- div:title-panel -->
## notXfSearch

<!-- div:left-panel -->

Имена и значения допполей для игнорирования показа новостей по допполям с указанными значениями.

**Синтаксис передачи данных:** `&notXfSearch=имя_поля|значение||имя_поля|значение`

?> Включение экспериментальных функций модуля повышает производительность  при использовании этого параметра.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?notXfSearch=name|value||name1|value1}
```




<!-- div:title-panel -->
## xfSearchLogic

<!-- div:left-panel -->
Логика фильтрации по значениям допполей: 
- "И" - совпадение нескольких значений; 
- "ИЛИ" - совпадение любого из значений;

Принимает `OR` или `AND`.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
&xfSearchLogic=OR
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?xfSearchLogic=AND}
```




<!-- div:title-panel -->
## catId

<!-- div:left-panel -->
 
Категории для показа (через запятую). 

Если указать **this** - новости будут браться из просматриваемой категории, при этом будет создаваться отдельный файл кеша для каждой категории.

Через тире указывается диапазон значений (от-до).
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?catId=5,6}
{include file="engine/modules/base/blockpro.php?catId=this}
{include file="engine/modules/base/blockpro.php?catId=2-6,10-15}
```




<!-- div:title-panel -->
## subcats

<!-- div:left-panel -->
Разрешает вывод подкатегорий для категорий, указанных в предыдущем параметре.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?subcats=y}
```




<!-- div:title-panel -->
## otCatId

<!-- div:left-panel -->
Игнорируемые категории (через запятую). 

Если указать **this** - новости будут браться из всех, кроме просматриваемой категории, при этом будет создаваться отдельный файл кеша для каждой категории.

Через тире указывается диапазон значений (от-до).
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?otCatId=5,6}
{include file="engine/modules/base/blockpro.php?otCatId=this}
{include file="engine/modules/base/blockpro.php?otCatId=2-6,10-15}}
```




<!-- div:title-panel -->
## notSubcats

<!-- div:left-panel -->
Разрешает игнорирование вывода из подкатегорий для категорий,  указанных в предыдущем параметре.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?notSubcats=y}
```




<!-- div:title-panel -->
## thisCatOnly

<!-- div:left-panel -->
Выводить/игнорировать новости **только** из текущей категории.

Вывод новостей только из текущей категории имеет смысл в тех случаях, когда используются мультикатегории и если нужно вывести или исключить из вывода новости, принадлежащие только к просматриваемой категории. 

К примеру похожие фильмы только из просматриваемой категории, а не из всех категорий, к которым принадлежит просматриваемый фильм.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?thisCatOnly=y}
```




<!-- div:title-panel -->
## tags

<!-- div:left-panel -->

Теги новостей, для фильтрации по ним (через запятую). 

Если указать **this** - будут браться новости в которых присутствует тег, при просмотре страницы конкретного тега, при этом будет создаваться отдельный файл кеша для каждой страницы тега.

Если указать `thisNewsTags` - будут браться новости в которых присутствуют теги текущей новости (имеет смысл только при просмотре полной новости).
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?tags=новости,события}
{include file="engine/modules/base/blockpro.php?tags=this}
{include file="engine/modules/base/blockpro.php?tags=thisNewsTags}
```



<!-- div:title-panel -->
## notTags

<!-- div:left-panel -->
Аналогично предыдущему пункту, но новости будут исключены из вывода.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?notTags=новости,события}
{include file="engine/modules/base/blockpro.php?notTags=this}
{include file="engine/modules/base/blockpro.php?notTags=thisNewsTags}
```





<!-- div:title-panel -->
## symbols

<!-- div:left-panel -->
 
Показ новостей, содержащих указанные символьные коды. 

Или **this** - для вывода новостей по просмариваемому символьному коду.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?symbols=a,A}
{include file="engine/modules/base/blockpro.php?symbols=this}
```




<!-- div:title-panel -->
## notSymbols

<!-- div:left-panel -->
Аналогично предыдущему пункту, но новости будут исключены из вывода.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?notSymbols=a,A}
{include file="engine/modules/base/blockpro.php?notSymbols=this}
```




<!-- div:title-panel -->
## day

<!-- div:left-panel -->
Временной период для отбора новостей, по умолчанию отсутствует
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?day=15}
```




<!-- div:title-panel -->
## dayCount

<!-- div:left-panel -->
Временной интервал для отбора новостей, по умолчанию отсутствует.

Для вывода новостей только за сегодня необходимо прописать `&day=-1&dayCount=-1`.

?> **Примечание:** <br> к примеру нужно вывести новости за прошлую неделю. Код: `&day=14&dayCount=7` выведет новости за период 14 дней с интервалом в 7 дней, что и есть прошлая неделя.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?dayCount=7}
{include file="engine/modules/base/blockpro.php?day=14&dayCount=7}
{include file="engine/modules/base/blockpro.php?day=-1&dayCount=-1}
```




<!-- div:title-panel -->
## future

<!-- div:left-panel -->
Режим афиши — вывод новостей только на ненаступившую дату. 

При этом параметры `&day` и `&dayCount` не вычитают, а прибавляют дни. 

!>Режим афиши не зависит от настроек DLE по выводу новостей на ненаступившую дату.

?> Например для вывода афиши на послезавтра нужно прописать `&future=y&day=3&dayCount=1`. 

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?future=y}
{include file="engine/modules/base/blockpro.php?future=y&day=3&dayCount=1}
```




<!-- div:title-panel -->
## sort

<!-- div:left-panel -->

Сортировка новостей в блоке, по умолчанию аналогична выводу ТОП-новостей.

**Возможные значения:**
- `none` - без сортировки (можно использовать для вывода похожих новостей идентично стандартному выводу таковых в DLE)
- `date` - по дате добавления
- `rating` - по рейтингу
- `comms` - по количеству комментариев
- `views` - по количеству просмотров
- `random` - в случайном порядке
- `randomLight` - в случайном порядке (Light) Предназначен для больших БД и органиченной выборки (с фильтрацией категорий, id новостей, допполей и т.п.)
- `title` - в алфавитном порядке
- `hit` - Хит. Новости отбираются по формуле: (рейтинг*100 + кол-во комментариев*10 + кол-во просмотров)
- `download` - по количеству скачиваний файлов новости
- `symbol` - по символьному коду новости
- `editdate` - по дате редактирования новости
- `xf|fieldname` - по значению дополнительного поля, где **fieldname** — название дополнительного поля.
- `symbol` - по символьному коду.
- `p.custom_field` - по нестандартному полю БД.

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false - стандартный для DLE топ новостей
```

Примеры использования:
```smarty
{* Сортировка по полю custom_field из таблицы dle_post *} 
{include file="engine/modules/base/blockpro.php?sort=p.custom_field} 

{* Сортировка по полю price из таблицы dle_post_extras *} 
{include file="engine/modules/base/blockpro.php?sort=e.price}

{* Сортировка по допполю price. Параметр xfilter=price - для отбрасывания пустых значений допполя *}
{include file="engine/modules/base/blockpro.php?xfilter=price&sort=xf|price&order=new"}
```




<!-- div:title-panel -->
## xfSortType

<!-- div:left-panel -->
Этот параметр необходимо указывать, если требуется сортировка по значению дополнительного поля, при этом указанное допполе содержит текст, а не цифры.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?xfSortType=string}
```




<!-- div:title-panel -->
## order

<!-- div:left-panel -->
Направление сортировки.

Djpvjжные значения: 
- `new` - новые в начале
- `old` - старые в начале
- `asis` - как есть. Выводит новости в том порядке, в котором они указаны в строке подключения. На данный момент она распространяется только на ID новостей.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
&order=new
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?order=new}
{include file="engine/modules/base/blockpro.php?order=old}
{include file="engine/modules/base/blockpro.php?order=asis}
```




<!-- div:title-panel -->
## avatar

<!-- div:left-panel -->
Разрешает вывод аватарки автора новости.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?avatar=y}
```




<!-- div:title-panel -->
## showstat

<!-- div:left-panel -->
Показывать статистику выполнения блока.
?> Статистика блока отображается только для админов
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?showstat=y}
```




<!-- div:title-panel -->
## related

<!-- div:left-panel -->
Включает модуль в режим отображения похожих новостей, переменная принимает id новости и тогда блок похожих новостей можно вывести даже в на странице с краткими новостями. 

Если же указать значение **this** - блок будет работать только в полной новости и показывать новости, похожие на просматриваемую
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?related=156}
{include file="engine/modules/base/blockpro.php?related=this}
```




<!-- div:title-panel -->
## saveRelated

<!-- div:left-panel -->
Записывать в БД похожие новости.

При первом обращении к старнице в БД будут записаны id выведенных похожих новостей, используя стандартный алгоритм DLE, при повторных обращениях (при отсутсвии кеша) данные будут браться из ранее записанных. 

Если нужно выводить и стандартные похожие новости и похожие новости через модуль — эту переменную использовать не нужно.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?saveRelated=y}
```




<!-- div:title-panel -->
## showNav

<!-- div:left-panel -->
Включить постраничную навигацию в блоке
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?showNav=y}
```




<!-- div:title-panel -->
## pageNum

<!-- div:left-panel -->
Текущая страница в блоке при загрузке страницы, при постраничной конфигурации.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?pageNum=5}
```




<!-- div:title-panel -->
## navStyle

<!-- div:left-panel -->
Стиль постраничной навигации.

**Возможны следующие стили:**

- `classic`: << Первая < 1 [2] 3 > Последняя >>
- `digg`: << Назад 1 2 ... 5 6 7 8 9 [10] 11 12 13 14 ... 25 26 Вперёд >>
- `extended`: << Назад | Страница 2 из 11 | Показаны новости 6-10 из 52 | Вперёд >>
- `punbb`: 1 ... 4 5 [6] 7 8 ... 15
- `arrows`: << Назад Вперёд >>
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
&navStyle=classic
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?navStyle=classic}
{include file="engine/modules/base/blockpro.php?navStyle=digg}
{include file="engine/modules/base/blockpro.php?navStyle=extended}
{include file="engine/modules/base/blockpro.php?navStyle=punbb}
{include file="engine/modules/base/blockpro.php?navStyle=arrows}
```



<!-- div:title-panel -->
## navDefaultGet

<!-- div:left-panel -->

Отслеживать стандартную навигацию DLE

При указании этого параметра модуль будет брать значение текущей страницы и формировать постраничную навигацию так же как это делается в DLE. Таким образом вы можете заменить тег `{content}` на строку подключения модуля в списках новостей, или просто организовать постраничную навигацию с перезагрузкой страницы.

?> **Кстати!** <br> Для замены стандартных шаблонов shortstory на шаблоны модуля сожно использовать [DLE-BlockProLight](https://github.com/dle-modules/DLE-BlockProLight)  
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?navDefaultGet=y}
```




<!-- div:title-panel -->
## fields

<!-- div:left-panel -->
Колонки, добавляемые в запрос на получение новостей

Префикс `p`. — колонка из таблицы `dle_post`, a `e.` — из таблицы `dle_post_extras`

Таким образом можно выводить данные из новостей даже если в БД DLE вносились дополнения.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?fields=p.custom,e.custom1}
```




<!-- div:title-panel -->
## setFilter

<!-- div:left-panel -->
Собственная фильтрация данных

Параметр предназначен для создания собственных условий фильтрации.
Корректность передачи данных не проверяется, будьте внимательнее при построении условий фильтрации.

Передавать каждый параметр фильтрации следует тремя частями разделяя их вертикальной чертой `|`.
Где:
- первая часть — поле из БД,
- вторая — оператор (см. ниже),
- третья — значение.

При этом параметры друг от друга следует отделять двойной вертикальной чертой `||`

Т.к. DLE, в целях безопасности, не позволяет передавать напрямую символы '>' и '<' через строку подключения, было принято решение использовать следующий порядок передачи операторов:
- `gt` или `+` — `>`
- `lt` или `-` — `<`
- `eq` или `=` — `=`
- `gte` или `+=` — `>=`
- `lte` или `-=` — `<=`
- `not` или `-+` или `+-` — `!=`
- `SEARCH` — `LIKE`
- `NOT_SEARCH` — `NOT LIKE`

Таким образом переданная строка
`p.comm_num|gt|100||e.news_read|lt|500`
превратится в часть запроса:
`p.comm_num > 100 AND e.news_read < 500`

Если третья часть параметра будет указана как `NOW()`, то будет подставлен текущий `timestamp`.

<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{* Новости, опубликованные в 2016 году. *}
{include file="engine/modules/base/blockpro.php?setFilter=YEAR(p.date)|eq|2016}

{* Новости, у которых дата начала события (нестандартное поле) больше или равна текущему моменту времени. *}
{include file="engine/modules/base/blockpro.php?setFilter=p.event_start|gte|NOW()}

{* Новости, в заголовке которых содержится словосочетание "Добро пожаловать". *}
{include file="engine/modules/base/blockpro.php?setFilter=p.title|SEARCH|Добро пожаловать}

{* Новости, у которых в заголовке нет текста "Добро пожаловать" *}
{include file="engine/modules/base/blockpro.php?setFilter=p.title|NOT_SEARCH|Добро пожаловать}
```




<!-- div:title-panel -->
## experiment

<!-- div:left-panel -->
Включает экспериментальные функции модуля. 

Этот параметр включает улучшенные, но не оттестированные до конца, функции модуля.
<!-- div:right-panel -->
Значение по умолчанию:
```smarty
false
```

Примеры использования:
```smarty
{include file="engine/modules/base/blockpro.php?experiment=y}
```




<!-- panels:end -->
