# GitHub Repository Statistics 

В рамках задания необходимо реализовать GUI приложение для 
получения данных о коммитах заданного GitHub репозитория.

## Получение данных 

Все данные программа должна получать через GitHub API.  
Для работы с private репозиториями требуется авторизация, 
для которой нужно получить токен на странице 
[https://github.com/settings/tokens/new](https://github.com/settings/tokens/new).
При генерации токена достаточно указать только scope `repo`. Токен нужен только для тестирования,
после тестирования его можно удалить на странице [https://github.com/settings/tokens/](https://github.com/settings/tokens/).  

**Не сохраняйте токен в репозитории!**

Запросы с авторизацией должны иметь заголовок `Authorization: Basic <авторизационный токен>`.
При этом `<авторизационный токен>` получается из логина пользователя и его токена 
как base64-кодированная строка `<username>:<password>`.

#### Получение списка коммитов

См. https://docs.github.com/en/free-pro-team@latest/rest/reference/repos#list-commits

#### Получение данных коммита  

См. https://docs.github.com/en/free-pro-team@latest/rest/reference/repos#get-a-commit

### Требования к приложению

Пользователь приложения указывает:
1. Логин в GitHub для авторизации
2. Токен для авторизации
3. URL репозитория (например `https://github.com/Kotlin/kotlinx.coroutines`) 

По этим данным после нажатия на кнопку `Load statistics` приложение должно строить таблицу вида: 

```
Author          Commits                    Files                               Changes
<Автор коммита> <Суммарное число коммитов> <Суммарное число затронутых файлов> <Суммарное число изменений>
```

Требования к реализации:

1. Нужно исключать коммиты, автор которых имел тип `Bot` 
2. Нужно исключать коммиты, сделанные более 12 месяцев назад 
3. Результаты в таблице нужно отсортировать по убыванию по числу коммитов  
4. Если один и тот же файл изменялся в разных коммитах, то считать его нужно один раз. При этом все изменения разных коммитов просто суммируются.
5. При загрузке данных UI не должен блокироваться
6. Таблица с результатами должна динамически обновляться по мере поступления данных
7. Нужно поддержать возможность отмены загрузки (кнопка `Cancel`)
8. Нужно использовать kotlinx.coroutines   

## Тесты

Необходимо реализовать тесты проверки корректности результатов с использованием `retrofit-mock`
