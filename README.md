## Домашнє завдання: SQL запити

У цьому завданні потрібно написати та виконати в **MySQL Workbench** декілька SQL-запитів до бази даних `mydb`.

---

### 1. Вибірка всіх стовпчиків з таблиці `products` та окремих стовпчиків з таблиці `shippers`

**Умова:**
- вибрати всі стовпчики (за допомогою wildcard `*`) з таблиці `products`;
- вибрати тільки стовпчики `name`, `phone` з таблиці `shippers`.

**Рішення:**

```sql
SELECT * FROM mydb.products;

SELECT name, phone FROM mydb.shippers;
```

---

### 2. Обчислення середнього, максимального та мінімального значення `price` в таблиці `products`

**Умова:**
- знайти середнє, максимальне та мінімальне значення стовпчика `price` таблиці `products`.

**Рішення:**

```sql
SELECT AVG(price) AS avg_price, 
       MAX(price) AS max_price,
       MIN(price) AS min_price
FROM mydb.products;
```

---

### 3. Унікальні значення `category_id` та `price` з сортуванням і обмеженням кількості рядків

**Умова:**
- обрати унікальні значення колонок `category_id` та `price` таблиці `products`;
- відсортувати за спаданням значення `price`;
- вивести тільки 10 рядків.

**Рішення:**

```sql
SELECT DISTINCT category_id, price 
FROM mydb.products
ORDER BY price DESC
LIMIT 10;
```

---

### 4. Кількість продуктів у цінових межах від 20 до 100

**Умова:**
- знайти кількість продуктів (рядків), які знаходяться в цінових межах від `20` до `100`.

**Рішення (варіант 1 — через умови порівняння):**

```sql
SELECT COUNT(*) AS products_count
FROM mydb.products
WHERE price >= 20 AND price <= 100;
```

**Рішення (варіант 2 — через `BETWEEN`):**

```sql
SELECT COUNT(*) AS products_count
FROM mydb.products
WHERE price BETWEEN 20 AND 100;
```

---

### 5. Кількість продуктів і середня ціна для кожного постачальника

**Умова:**
- знайти кількість продуктів (рядків) та середню ціну (`price`) у кожного постачальника (`supplier_id`).

**Рішення:**

```sql
SELECT supplier_id,
       COUNT(*) AS products_count,
       AVG(price) AS avg_price
FROM mydb.products
GROUP BY supplier_id
ORDER BY products_count;
```

