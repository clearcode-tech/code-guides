## Java Rule 1: Слои бизнес-логики


Слои проекта:
- controller - Контроллер, в общепринятом понимании. На этом уровне можно взаимодействовать
со слоями: <b>validator и controller service</b>
- controller service - Сервисный слой, в котором можно подготовить данные полученные из контроллера
или валидатора в пригодный вид. Например: типизировать ID или извлечь данные из кеша. На этом уровне можно
взаимодействовать со слоями: <b>manager и service</b>
- validator - Слой проверяющий входные данные и права. Может вернуть кеш, как результат своей работы.
На этом уровне можно взаимодействовать со слоями: <b>validations и service</b>
- validations - Сервисный слой, куда вынесены require методы проверяющие входные данные и права.
На этом уровне можно взаимодействовать со слоями: <b>client, service и другими validations</b>
- client - Клиент модуля, в общепринятом понимании. На этом уровне можно взаимодействовать со слоями:
<b>manager и service</b>
- manager - Слой для бизнес-методов, в которых содержится основная логика. На этом уровне можно взаимодействовать
со слоями: <b>client, service и другими manager.</b>
- service - Слой для методов содержащих логику взаимодействия с моделями. На этом уровне можно взаимодействовать
со слоями: <b>repository и другими service</b>
- repository - Репозиторий, в общепринятом понимании.


#### Правила работы внутри слоёв

1. Создание и обновление модели (.toBuilder и .build) лучше производить внутри метода на уровне Service.