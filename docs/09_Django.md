# Django

- django auth
    - user
- content-type

## ORM

- Lazy-evaluation - выполнение только когда нужно
- Auto commit mode - каждый save вызывает коммит

### Оптимизации

- `.select_related` - join
- `.fetch_related` - неск. запросов

### Транзакции

- `@ / with transaction.atomic` - все или ничего
- `ATOMIC_REQUESTS` - все будет атомарным per-request
- `transaction.on_commit` - выполнение кода после успешного коммита
- `DATABASES['default']['OPTIONS']['isolation_level']`  - выставление уровня транзакции

## DRF

### Serializers

- SerializerMethodField - read-only поля