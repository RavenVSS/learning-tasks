# Задача. Асинхронная конвертация файлов

### Аргументация
Если сервисом будут пользоваться часто, по 1000 запросов в минуту, а у нас машина слабая, то желательно делать асинхронную обработку.

### Хвосты
| URL | Возвращаемое значение | Описание |
| ----------------------- | ----------- | ----------- |
| POST /convert-to-webp/async | UUID | Запрос возвращает UUID задачи на конвертацию |
| GET /convert-to-webp/async/{UUID}/status | TaskStatus, ErrorMessage | Возвращает статус конвертации SUCCESS, ERROR или PROCESSING, если ERROR, то информация об ошибке |
| GET /convert-to-webp/async/{UUID} | File | Возвращает файл, либо 404 статус, если конвертация ещё не завершена или ошибка |

### Требования
- хранить задачи в БД PostgreSql
- обработка должна выполняться независимо от запросов (в отдельных потоках)
- наличие интеграционных тестов: на все 3 запроса, на обработчик задач
- файлы хранить в отдельных папках (in, out), важно, чтобы одинаковое название файлов не влияло на работу сервиса
- после успешной обработки исходный файл удалять сразу, а результат хранить в течении N времени (настраивается через конфиг)

### Вариант реализации
Через планировщик задач, который каждые N времени будет обрабатывает все актуальные задачи из БД.  

![Диаграмма](/task-1.png)

### Почитать
- [Подключение PostgreSql в Spring](https://www.bezkoder.com/spring-boot-postgresql-example/)
- [JPA репозитории](https://www.baeldung.com/spring-data-repositories)
- [Планировщик задач](https://www.baeldung.com/spring-scheduled-tasks)
- [Конфигурация сервиса через @Value](https://www.baeldung.com/spring-value-annotation)
- [Jupiter-Tools. Библиотека для интеграционных тестов PostgreSql](https://github.com/jupiter-tools/spring-boot-extensions?tab=readme-ov-file#postgresql-extension)
- [Database Rider. Библиотека для проверки/добавления значений в БД](https://github.com/database-rider/database-rider?tab=readme-ov-file#expected-dataset) (уже имеется в Jupiter-Tools)
