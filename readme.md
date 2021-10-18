# Что такое git
___Система контроля версий (VCS)___ - ПО для пошагового изменения файла, переключения между версиями файла, сегментирвоания файла.
* Полная история изменений каждого файла за длительный период. Это касается всех изменений, внесенных огромным количеством людей за долгие годы. Изменением считается создание и удаление файлов, а также редактирование их содержимого. Различные инструменты VCS отличаются тем, насколько хорошо они обрабатывают операции переименования и перемещения файлов. В историю также должны входить сведения об авторе, дата и комментарий с описанием цели каждого изменения. Наличие полной истории позволяет возвращаться к предыдущим версиям, чтобы проводить анализ основных причин возникновения ошибок и устранять проблемы в старых версиях программного обеспечения.
* Ветвление и слияние. Создание «веток» позволяет иметь несколько независимых друг от друга направлений разработки, а также выполнять их слияние, чтобы разработчики могли проверить, что изменения, внесенные в каждую из веток, не конфликтуют друг с другом. Многие команды разработчиков программного обеспечения создают отдельные ветки для каждой функциональной возможности, для каждого релиза либо и для того, и для другого.


# Подготовка репозитория
1.	Скачать и установить VS Code [отсюда](https://code.visualstudio.com/docs/?dv=win)
2.	Скачать и установить Git [по ссылке](https://git-scm.com/download/win)
3.	Проверить, работает ли git  с помощью команды 
git --version
4.	Добавить имя и email пользователя с помощью команд
  git config --global user.email "email@mail.com"
  git config --global user.name "User Name"


# Создание «сохранений»

**git add**

Команда `git add` добавляет изменение из рабочего каталога в раздел проиндексированных файлов. Она сообщает Git, что вы хотите включить изменения в конкретном файле в следующий коммит. Однако на самом деле команда `git add` не оказывает существенного влияния на репозиторий: изменения регистрируются в нем только после выполнения команды `git commit`.

    (здесь что-то умное по теме)
    Ошибки, конфликты, больше ошибок.

# Перемещение между сохранениями
Команда git checkout используется для переключения веток и выгрузки их содержимого в рабочий каталог.

Мы познакомились с этой командой в разделе Переключение веток главы 3 вместе с git branch.

В разделе Отслеживание веток главы 3 мы узнали как использовать флаг --track для отслеживания веток.

В разделе Использование команды checkout в конфликтах главы 7 мы использовали эту команду с опцией --conflict=diff3 для разрешения конфликтов заново, в случае если предыдущее решение не подходило по некоторым причинам.

Мы рассмотрели детали взаимосвязи этой команды и git reset в разделе Раскрытие тайн reset главы 7.

Мы исследовали внутренние механизмы этой команды в разделе HEAD главы 10. Информация [отсюда](https://git-scm.com/book/ru/v2/%D0%9F%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5-C%3A-%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D1%8B-Git-%D0%92%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B8-%D1%81%D0%BB%D0%B8%D1%8F%D0%BD%D0%B8%D1%8F).

### Запись от себя.

Сохранив изменения, можно ввести команду ___git log___, которая выведет историю изменений с именами сохранений (строка начинается с "commit"). Чтобы переместиться между двумя имеющимися в репозитории сохранении, нужно ввести команду ___git checkout (первые 4 символа имени сохранения)___.

# Журнал изменений

### Взято [тут](https://git-scm.com/docs/git-log).

Shows the commit logs.

List commits that are reachable by following the parent links from the given commit(s), but exclude commits that are reachable from the one(s) given with a ^ in front of them. The output is given in reverse chronological order by default.

You can think of this as a set operation. Commits reachable from any of the commits given on the command line form a set, and then commits reachable from any of the ones given with ^ in front are subtracted from that set. The remaining commits are what comes out in the command’s output. Various other options and paths parameters can be used to further limit the result.
Thus, the following command:

$ git log foo bar ^baz
means "list all the commits which are reachable from foo or bar, but not from baz".

A special notation "<commit1>..<commit2>" can be used as a short-hand for "^<commit1> <commit2>". For example, either of the following may be used interchangeably:

$ git log origin..HEAD
$ git log HEAD ^origin
Another special notation is "<commit1>…​<commit2>" which is useful for merges. The resulting set of commits is the symmetric difference between the two operands. The following two commands are equivalent:

$ git log A B --not $(git merge-base --all A B)
$ git log A...B
The command takes options applicable to the git-rev-list[1] command to control what is shown and how, and options applicable to the git-diff[1] command to control how the changes each commit introduces are shown.
### Инфа от себя.
Команда ___git log___ открывает журнал изменений, где указано, например:
commit ff9efc03fdc2b15bd83b2852c650d4072ce3445a - имя изменения, используя которое в команде ___git checkout___, можно переместиться в интересуемую версию репозитория.

Author: Роман Ахметов <roman3202@gmail.com> - имя автора, создавшего изменение.

Date:   Mon Oct 18 10:54:02 2021 +0300 - дата в время сохдания изменения.

# Ветки в git
### Инфа от себя.
При работе нескольких человек с репозиторием, полезно сегментировать изменения, которые хотят внести в файл участники. Для этого используется команда ___git branch___, выводящая список созданных веток, а команда ___git branch (название новой ветки)___ создаёт новую ветку. Важно помнить, что следует сохранять информацию во всех ветках.

# Слияние веток и решение конфликтов
# Удаление веток
