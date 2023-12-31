# Введение в GIT 

Одна из самых популярных **систем контроля версий**. 
Альтернативы — `Mercurial`, `SVN`.
Такие системы позволяют вести распределённую разработку.

## Зачем нужно?

- Хранение истории измений
- Командная разработка проекта
- Синхронизация между устройствами одного разработчика

## Создание репозитория

Дальнейшие команды будут происходить с [репозиторием](https://github.com/DrEternity/Hello_world)

Два основных способа создать репозиторий:
1. Создать его локально. Затем, опционально, его можно "подключить" к удалённой версии репозитория
2. Создать удалённый репозиторий с помощью **онлайн-сервисов** (`GitHub`, `Bitbucket`,...). Затем, "склонировать" его локально на компьютер.

Создадим репозиторий с помощью сервиса [GitHub](https://github.com) и скопируем его себе на компьютер.
```cpp

git clone git@github.com:DrEternity/Hello_world.git
```
ссылку на репозиторий вы найдёте нажав на зелёный виджет с надписью `code`

В `GitHub` есть разграничение прав на работу с репозиториями. Можно задавать различные политики: сделать репозиторий публичным и приватным, ограничить права кругу пользователей или кому-то одному, например, разрешить просматривать репозиторий, но не изменять в нём данные.

Для дальнейшей работы с репозиторием через `SSH` необходимо сгенерировать ключи шифрования и добавить публичный в [найстройки](https://github.com/settings/keys). 
Как генерировать ключ, смотрите в главе про `SSH`

## Рабочая зоны

### Проверка состояния

Начнём работу в пустом рабочем каталоге. 
Используем команду `git status`, чтобы проверить текущее состояние репозитория
```cpp
git status 
```
Вы увидите:
```cpp
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```
Команда проверки состояния сообщит, что коммитить нечего. Это означает, что в репозитории хранится текущее состояние рабочего каталога, и нет никаких изменений, ожидающих записи.

### Внесение изменений

Создадим файл **hello.cpp** и заполним его:
```cpp
#include <iostream>
int main(int argc, char** argv)
{
	std::cout << "Hello, World!" << std::endl;
	return 0;
}
```
Теперь, проверив состояние командой `git status`, получим:
```cpp
On branch main
Your branch is up to date with 'origin/main'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	hello.cpp

nothing added to commit but untracked files present (use "git add" to track)
```
Первое, что нужно заметить, это то, что git знает, что файл `hello.cpp` был изменен, но при этом эти изменения еще не зафиксированы в репозитории.

Также обратите внимание на то, что сообщение о состоянии дает вам подсказку о том, что нужно делать дальше. Если вы хотите добавить эти изменения в репозиторий, используйте команду `git add`. В противном случае используйте команду `git сheckout` для отмены изменений.

### Индексация изменений

Теперь дадим команду git проиндексировать изменения. Проверьте состояние:
```cpp
git add hello.cpp
git status
```
И вы увидите:
```cpp
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   hello.cpp
```
Изменения файла `hello.cpp` были проиндексированы. Это означает, что git теперь знает об изменении, но изменение пока не _перманентно_ записано в репозиторий. Следующий коммит будет включать в себя проиндексированные изменения.

Если вы решили, что _не_ хотите коммитить изменения, команда состояния напомнит вам о том, что с помощью команды `git reset` можно снять индексацию этих изменений.

### Индексация и коммит

Отдельный шаг индексации в git позволяет вам продолжать вносить изменения в рабочий каталог, а затем, в момент, когда вы захотите взаимодействовать с версионным контролем, git позволит записать изменения в малых коммитах, которые фиксируют то, что вы сделали.

Предварительно укажем ваше имя для хранения информации о владельце коммита:
```cpp
git config --global user.name "Your Name"
```
Для начала сделаем коммит относящийся к созданию файла `hello.cpp` :
```cpp
git commit -m "Creating hello.cpp"
```
Получим:
```cpp
[main 06c8061] Creating hello.cpp
 1 file changed, 6 insertions(+)
 create mode 100644 hello.cpp
```
После этого проверим статус репозитория:
```cpp
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
Рабочий каталог чистый, можно продолжать работу.

### Push на GitHub

Для применения изменений на странице репозитория Github необходимо восзпользоваться командой `git push`:
```cpp
git push
```
И получим:
```cpp
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 378 bytes | 378.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:DrEternity/Hello_world.git
   1e34520..ea98947  main -> main
```
Теперь созданный нами файл можно найти на странице репозитория на GitHub

Таким образом, для внесения изменений в репозиторий вам необходимо в начале индексировать изменения командой `add`, а затем делать `commit` добавленных изменений. Разделяя индексацию и коммит, вы имеете возможность с легкостью настроить, что идет в какой коммит. А для изменений состояний репозитория на GitHub необходимо дополнительно делать `push`. 

В этом кратком обзоре вы и близко не познакомились со всеми возможностями системы контроля версий `git`. Однако на данный момент вам этого достаточно. О тонкостях настройки `git` под себя и других возможностях связанных с совместной разработкой можете почитать [здесь]()
