## Java Rule 2: Java классы



#### Общие правила для классов

1. Если класс может быть финализирован, то следует это сделать.

2. Используем аннотации lombok и javax для облегчения кода.

3. Не используем setter, чтобы не нарушать иммутабельность.


#### Правила для моделей (Entity)

1. Используем аннотации:
- lombok.AllArgsConstructor(access = AccessLevel.PRIVATE) для добавления конструктора, содержащего все поля класса в качестве параметров (без необходимости не расширяем видимость конструктора).
- lombok.NoArgsConstructor(access = AccessLevel.PRIVATE, force = true) для добавления конструктора без параметров (без необходимости не расширяем видимость конструктора).
- lombok.Builder или SuperBuilder (если есть наследование) для возможности инстанцирования объекта паттерном Builder.
- lombok.Getter для доступа к значениям полей класса.
- lombok.EqualsAndHashCode(callSuper = true, onlyExplicitlyIncluded = true) для переопределения equals и hashcode объекта.
- javax.persistence.Entity для обозначения сущностей.
- lombok.FieldNameConstants для удобства работы с БД - для всех полей класса делаем enum отображение.

2. Модели (Entity) наследуем от BaseModel.
