## Common Rule 4: Комментирование сущностей

Комментируем всё кроме:
- `@Override` методов, если комментарий в базовом классе полностью описывает логику метода. Однако комментарий нужен, если надо указать специфику реализации метода.
- Конструкторов классов.
- Полей классов, если это сложные классы, такие как репозитории, сервисы, клиенты и т.д. Хорошим признаком того, что поле не нуждается в комментарии, является то, что значение для поля заполняется средствами DI-контейнера автоматически (т.е. используется аннотация `@Inject`). Более специфичные поля в классах нуждаются в комментировании, например, поля в классах моделей, DTO и т.д.

Правило касается и Java и Typescript.

Соглашение к подходу комментирования методов: 

- Первое предложение описывает суть метода и является отдельным абзацем.
- Первое предложение начинается с глагола. 
  - Для методов, возвращающих boolean, первое предложение является вопросом, на который отвечает метод.
- Остальное описание в отдельном(ых) абзацах.
- Для перечисления стоит использовать `<ul><li>...</li></ul>`.
- HTML-теги используются только в Java.

Общие правила:

- В конце всех предложений ставится точка.
- Для подсказок об опечатках, пропущенных или лишних запятых рекомендуется настроить IDEA в разделе `Settings` > `Editor` > `Proofreading`. Необходимо добавить поддержку русского языка, если она отсутствует. В подразделе `Grammar` настроить типы файлов, в которых должна работать проверка орфографии и пунктуации.
- Стоит переиспользовать один и те же фразы или слова, когда описание касается чего-то, что уже было где-то упомянуто. Это позволяет:
  - Иметь единый стиль.
  - Не тратить силы на продумывание каждый раз нового описания.