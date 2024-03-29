## Angular Rule 6: Сервисы и derivations

### Service - сервис для работы с моделью данных или логикой, объединенной общим контекстом

- Методы в рамках одного сервиса должны быть объединены по семантике. Например, сервис для работы с моделью, с датами, 
фильтрами определенного реестра, определенным диалогом и т.д.
- Чаще всего методы сервиса вызываются из effect'ов, ts-компонентов, reducer'ов. 
- Методы не должны принимать в качестве параметров состояние приложения. То есть при вызове из reducer'ов необходимо 
передать в сервис конкретное поле состояния или их список, а также данные для обновления.
- Если в рамках метода необходимо работать с другой моделью или другим контекстом, должен быть реализован вызов метода 
другого сервиса. Пример: Метод обновления сотрудника в сервисе обновляет также его каналы уведомлений. Правильным решением будет 2 метода - основной 
метод относится к сервису для работы с сотрудником, а внутри него вызывается метод сервиса для работы с каналами 
уведомлений.
- Расположение: _src/modules/root/services/_. Для сервисов диалогов: _src/modules/root/services/dialogs_.

### Derivations - функции для получения данных на основе состояния приложения

- Методы объединены контекстом одного state'а.
- Методы принимают в качестве одного из аргументов state.
- Чаще всего методы вызываются из guard'ов и selector'ов.
- Расположение: _src/modules/root/store/derivations_.

#### Наиболее распространенные методы Derivations:

- ```static loaded(state: SomeState): boolean;``` <br>
Определяет, что состояние уже загружено. Чаще всего определяется по основному полю состояния 
(```return (state.someField !== undefined)```).
- ```static failed(state: SomeState): boolean;``` <br>
Определяет, что при выполнении загрузки произошла ошибка. Чаще всего определяется по полю ошибки 
(```return !!state.error;```).
- ```static needToBeLoaded(state: SomeState): boolean;``` <br>
Определяет, нужно ли загрузить состояние. Чаще всего определяется как 
  ```
  return (
      !state.loading
      && !SomeStateDerivations.loaded(state)
      && !SomeStateDerivations.failed(state)
  )
  ```
