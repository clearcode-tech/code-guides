## Java Rule 5: Try-catch

1. Каждый метод должен обрабатывать ошибку внутри себя. Проброс ошибок `throws SomeException` в методах запрещён.
Даже если это приватный метод, который вызывается единожды внутри try-catch.

    ```
    ...
    public DTO createRequest(...) {
    
        try {
    
            this.doSomething(...);
            this.doSomethingElse(...);
        }
        catch (Exception e) {
    
            throw new RequestException("message", e);
        }
    }
    
    private void doSomething(...) {
    
        try {
    
            ...
        }
        catch (IncorrectInputDataException e) {
    
            throw new IllegalStateException("message", e);
        }
    }
    
    private void doSomethingElse(...) {
    
        ...
        try {
    
            ...
        }
        catch (InterruptedException e) {
    
            Thread.currentThread().interrupt();
            throw new IllegalStateException("Request to something was interrupted", e);
        }
    }
    ...
    ```

2. Каждый метод, содержащий операции, которые подразумевают атомарность, должен иметь свою транзакцию.
Даже если это приватный метод, который вызывается единожды внутри транзакции.

    ```
    ...
    public DTO createRequest(...) {
    
        try (Transaction transaction = this.tenantTransactionProvider.get(tenantId)) {
    
            this.doSomething(...);
            this.doSomethingElse(...);
    
            transaction.commit();
        }
    }
    
    private void doSomething(...) {
    
        try (Transaction transaction = this.tenantTransactionProvider.get(tenantId)) {
    
            ...
    
            transaction.commit();
        }
    }
    
    private void doSomethingElse(...) {
    
        ...
        try (Transaction transaction = this.tenantTransactionProvider.get(tenantId)) {
    
            ...
    
            transaction.commit();
        }
    }
    ...
    ```