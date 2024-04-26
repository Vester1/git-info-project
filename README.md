# Шпаргалка по гиту

---
## Основные команды
## Навигация
* `pwd` - Выводит путь нынешней директории
* `ls` - Выводит все файлы в нынешней папке  
   с флагом `ls -a` выведет *дополнительно* скрытые папки и файлы
* `cd /first-project` - Переход в папку *first-project*  
  `cd ..` - Переход на папку выше  
  `cd ~` - Переход в домашнюю директорию

---
## Работа с файлами и папками
### Создание, удаление, перемещение
* `touch draft1.txt` - Создает файл *draft1.txt*
* `mkdir dev` - Создает папку *dev*
* `rm draft1.txt` - Удаляет файл *draft1.txt*
* `rmdir dev` - Удаляет папку (**если пустая**)
* `rm -r dev` - Удаляет папку вместе с содержимым
* `cp draft1.txt ~/Desktop` - Копирует файл в указанную папку
* `mv draft1.txt ~/git1` - Перемещает файл в указанную папку

---
## Работа с github
* `git init` - Инициализация репозитория в нынешней папке
* `git remote add origin git@github.com:...` - Привязка локального репозитория к удаленному  
  `git remote -v` - Просмотр соединений локального репозитория с удаленным
* `git status` - Просмотр изменений в репозитории
* `git add --all` - *Запоминание* содержимого всех файлов
* `git commit -m "Комментарий"` - *Сохранение* в историю изменений файлов  
  `git commit --ammend --no-edit` - флаг `ammend` позволяет добавить в последний коммит новые файлы
или изменения в нынешних. Флаг `no-edit` оставляет комментарий без изменений
* `git log` - История коммитов  
  `git log --oneline`- Сокращенный лог
* `git push main/master` - Загрузка файлов на удаленный репозиторий  
  `git push -u origin master/main` - **При первом push нужно использовать эту команду**
* `git restore --staged <file>` - Удаление файла из *'staging area'*. Вместо `<file>`
можно поставить `.` чтобы удалить все файлы в папке.
* `git reset --hard <hash>` - Откат проекта до этого коммита(то есть этот коммит станет
**HEAD**), а более поздние коммиты удалятся
* `git restore <file>` - Если случайно изменили файл, и он попал в *modified*, его 
можно откатить этой командой
* `git diff` - Просмотр изменений *modified* файлов  
  Если нужно посмотреть *staged* файлы, то нужно добавить флаг `--staged`
* `git diff <hash1> <hash2>` - Сравнение двух коммитов(вместо `<hash2>` можно вставить **HEAD**)  
  Также можно сравнивать ветку и другой коммит(или ветку с веткой), указав имя ветки
### Работа с ветками
* `git clone git@github.com:..` - Клонирование удаленного репозитория себе на компьютер 
* `git branch` - Просмотр веток проекта(звёздочкой будет помечена ветка,
в которой вы сейчас находитесь)  
  `git branch <название_ветки>` - Создание новой ветки
* `git checkout <название_ветки>` - Переключение на указанную ветку  
  `git checkout -b <название_ветки>` - Создание новой ветки и переключение на неё
* `git diff <ветка1> <ветка2>` - Сравнение двух веток или ветки и коммита
  
---
## Основные понятия
* **Хеш** - это основной идентификатор коммита,
из него можно получить автора, дату и содержимое файлов
* **Лог** - это история коммитов проекта (команда - `git log`(см. *Основные команды*))
* **HEAD** - это файл в .git, указывающий на последний коммит.  Если нужно передать в функцию
последний коммит, то вместо его хеша можно просто написать слово *HEAD*
* **Статусы файлов в git**  
  * *untracked* - Только добавленный файл в папку проекта. У гита нет информации про него  
  * *staged* - После выполнения команды git add файл попадает в staging area,
то есть в список файлов, которые войдут в коммит
  * *tracked* - Все файлы, версии которых уже отслеживает гит
  * *modified* - Файл содержит изменения по сравнению с прошлой версией
* **Git status**
  * *staged* (Changes to be committed)
  * *modified* (Changes not staged for commit)
  * *untracked* (Untracked files)
* **Оформление сообщений к коммитам**  
  Нужно писать информативные и понятные комментарии длиной не более 72 символов  
  Пример хороших сообщений:
  * Исправление опечатки в заголовке главной страницы на хорватском
  * Добавлена сортировка по полю «Сумма»
  * Оптимизирована загрузка фотографий в галерее  
* **Работа над ошибками в коммитах**  
  * Исправление коммита  
    Вы добавили два файла в папку репозитория, *main.html* и *common.css*, но
вы забыли про второй и закоммитили только первый. Чтобы не делать ещё один коммит,
нужно воспользоваться командой `git commit --amend --no-edit`(предварительно добавив
*common.css* в *'staging area'*)  
  Если нужно добавить новый комментарий, то вместо `--no-edit` нужно написать  
`-m "Новое сообщение"`
* **Файл `.gitignore`**  
  Чтобы Git игнорировал такие файлы и не пытался добавить их в репозиторий,
нужно создать файл `.gitignore` и записать в него названия игнорируемых файлов.  
  * *Название файла* - чтобы игнорировать какой-то файл, нужно просто добавить его название
  * *Звёздочка(`*`)* - Соответствует любой строке, включая пустую  
    ```.gitignore
    # игнорировать все файлы, которые заканчиваются на .jpeg
    *.jpeg

    # игнорировать все файлы "tmp" во всех подпапках папки docs
    docs/*/tmp
    ```
  * *Вопросительный знак(`?`)* - Обозначает *один* любой символ  
    `file?.txt` - будут проигнорированы `fileA.txt`, `file5.txt`, *но не* `fileA5.txt`
  * *Квадратные скобки(`[..]`)* - Обозначет один символ из списка `[012]` или диапазона `[0-9]`
  * *Слеш(`/`)* - Указывает на каталоги  
    Если `.gitignore` начинается со слеша, о Git проигнорирует файлы или каталоги только в корневой директории  
    ```.gitignore
    # игнорировать todo.txt в корне репозитория, но файл dir1/todo.txt останется
    /todo.txt
  
    # для сравнения: spam.txt будет игнорироваться во всех папках
    spam.txt
    ```
    Если шаблон заканчивается слешем, то правило применится только к папке  
    `build/` - если `build` — это папка, то она будет проигнорирована. Если `build` — обычный файл,
    то он не подпадёт под правило и не будет игнорироваться
  * *Парные звёздочки(`**`)* - Функция парных звёздочек (**) похожа на функцию одинарной (*).
    Отличие в том, как они работают с вложенными папками. Двойная звёздочка может соответствовать любому количеству
    таких папок (в том числе нулю). Одинарная может соответствовать только одной
    ```.gitignore
    # игнорировать файлы "docs/current/tmp", "docs/old/tmp",
    # а также "docs/old/saved/a/b/c/d/tmp"
    # и даже "docs/tmp", потому что ноль вложенных папок тоже подходит
    docs/**/tmp
    
    # игнорировать только "docs/current/tmp" и "docs/old/tmp"
    # файл "docs/old/saved/a/b/c/d/tmp" не попадает в правило
    docs/*/tmp 
    ```
  * *Восклицательный знак(`!`)* - Инвертирование(`!doge.jpeg` - Оставь этот файл в любом случае)
* **Fork** - это GitHub-операция; напрямую с Git она не связана. «Форк» создаёт копию
  репозитория в аккаунте GitHub. Такая копия будет полностью независима. Изменения,
  которые вы внесёте, не будут синхронизированы с исходным репозиторием.
* **Ветки**  
  Ветка - это изолированный поток разработки проекта. В таком потоке можно проверять
разные идеи, тестировать новую функциональность и так далее.  
  Суффикс навигации `~`  
  Для облегчения этой задачи в Git есть суффикс навигации ~N, где N — это число.
Он отсчитывает от заданного коммита N коммитов назад во времени.
Нумерация начинается с нуля: **commit~0** — это сам коммит, **commit~1** — предыдущий,
**commit~2** — предшествующий предыдущему и так далее.  
  Например, **HEAD~1** — это следующий за текущим коммит. А **main~5** — это пятый коммит
в ветке main, если считать с последнего выполненного коммита.  
  Для **~1** есть специальное сокращение **~** (без числа). То есть вместо **HEAD~1**
обычно пишут просто **HEAD~**.

 