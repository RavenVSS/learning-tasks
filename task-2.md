# Задача. Обработка исключений через @ControllerAdvice

### Аргументация
Для удобной обработки валидации, бизнесовых ошибок и т.п. удобно использовать Java исключения (как кастомные, так и встроенные).  
Чтобы выводить чиаемые ошибки в любом месте выполнения программы, можно вызывать определённые исключение с описанием ошибки.

### Требования
- Наличие @ControllerAdvice
- При любой ошибке в ответе за запрос всегда должен отправляться ErrorDto
- В моментах, когда "сущность не найдена" кидать исключение
- При бизнесовых ошибках, кидать исключение
- Валидация через аннотации @Valid или @Validated (опционально)

### Почитать
- [Обработка исключений в REST API SpringBoot](https://www.bezkoder.com/spring-boot-postgresql-example/)](https://struchkov.dev/blog/ru/exception-handling-controlleradvice/)
- [Validation in Spring Boot](https://www.baeldung.com/spring-boot-bean-validation)
