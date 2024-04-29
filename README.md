# Домашнее задание № 28 по теме: "Репликация mysql". К курсу Administrator Linux. Professional

## Задание

- Настроить репликацию MySQL
- Приложить логи и рабочий vagrant-стенд

## Выполнение

После разворачивания стенда:

```bash
vagrant ssh source -c 'mysql -uroot -pOtus2023! -e "use bet; show tables;"'
```

```
+------------------+
| Tables_in_bet    |
+------------------+
| bookmaker        |
| competition      |
| events_on_demand |
| market           |
| odds             |
| outcome          |
| v_same_event     |
+------------------+
```

```bash
vagrant ssh source -c 'mysql -uroot -pOtus2023! -e "use bet; select * from bookmaker;"'
```

```
+----+----------------+
| id | bookmaker_name |
+----+----------------+
|  4 | betway         |
|  5 | bwin           |
|  6 | ladbrokes      |
|  3 | unibet         |
+----+----------------+
```

```bash
vagrant ssh source -c "mysql -uroot -pOtus2023! -e \"use bet; INSERT INTO bookmaker (id,bookmaker_name) VALUES(1,'1xbet');\""
```

```bash
vagrant ssh source -c 'mysql -uroot -pOtus2023! -e "use bet; select * from bookmaker;"'
```

```
+----+----------------+
| id | bookmaker_name |
+----+----------------+
|  1 | 1xbet          |
|  4 | betway         |
|  5 | bwin           |
|  6 | ladbrokes      |
|  3 | unibet         |
+----+----------------+
```

```bash
vagrant ssh replica -c 'mysql -uroot -pOtus2023! -e "use bet; select * from bookmaker;"'
```

```
+----+----------------+
| id | bookmaker_name |
+----+----------------+
|  1 | 1xbet          |
|  4 | betway         |
|  5 | bwin           |
|  6 | ladbrokes      |
|  3 | unibet         |
+----+----------------+
```

### Делаем вывод - репликация настроена.