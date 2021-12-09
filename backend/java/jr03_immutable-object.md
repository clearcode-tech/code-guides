## Java Rule 3: Неизменяемые объекты



1. Коллекции, извлечённые из БД, следует обернуть в иммутабельную обёртку перед передачей их в следующие слои.

Примеры обёрток:
`List.copyOf(someItems);`
`someStream.collect(Collectors.toUnmodifiableList())`

2. Поля класса должны быть финализированы.

3. С моделями и ДТО работаем через builder, потому что он создаёт новый экземпляр с изменёнными полями.