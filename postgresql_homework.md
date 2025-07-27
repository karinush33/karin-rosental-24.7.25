# PostgreSQL Homework Solutions 📘

## 1. AUTOINCREMENT

```sql
CREATE TABLE members (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    full_name TEXT NOT NULL
);

INSERT INTO members (id, full_name) VALUES
(101, 'Shira Levi'),
(102, 'Nadav Cohen'),
(103, 'Yael Azulay');

INSERT INTO members (full_name) VALUES ('nir choen');
INSERT INTO members (full_name) VALUES ('Bob_marley');
INSERT INTO members (full_name) VALUES ('Tal Ben Haim');
```

---

## 2. UNION

```sql
CREATE TABLE patients (
    id INTEGER PRIMARY KEY,
    name TEXT
);

CREATE TABLE nurses (
    id INTEGER PRIMARY KEY,
    name TEXT
);

INSERT INTO patients (name) VALUES ('Yoni'), ('Dana'), ('Avi');
INSERT INTO nurses (name) VALUES ('Avi'), ('Tamar'), ('Lior');

SELECT name FROM patients
UNION
SELECT name FROM nurses;
```

---

## 3. ON DELETE CASCADE

```sql
PRAGMA foreign_keys = ON;

DROP TABLE IF EXISTS movies;
DROP TABLE IF EXISTS directors;

CREATE TABLE directors (
    director_id INTEGER PRIMARY KEY,
    name TEXT
);

CREATE TABLE movies (
    movie_id INTEGER PRIMARY KEY,
    title TEXT,
    director_id INTEGER,
    FOREIGN KEY(director_id) REFERENCES directors(director_id) ON DELETE CASCADE
);

INSERT INTO directors (name) VALUES ('Spielberg');
INSERT INTO movies (title, director_id) VALUES ('Jaws', 1);

DELETE FROM directors WHERE director_id = 1;
```

---

## 4. SERIAL

```sql
DROP TABLE IF EXISTS trainers;

CREATE TABLE trainers (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL
);

INSERT INTO trainers (id, name) VALUES
(201, 'Erez Barak'),
(202, 'Liat Ben-Haim'),
(203, 'Gil Oren');

-- מוסיפים רשומות נוספות ללא ציון מזהה:
INSERT INTO trainers (name) VALUES
('karin rozental'),
('yotam livne'),
('dan katz');
```

---

## 5. INSERT with RANDOM

```sql
CREATE TABLE measurements (
    id SERIAL PRIMARY KEY,
    value NUMERIC(5,2)
);

INSERT INTO measurements (value) VALUES
(round((random() * 10 + 5)::numeric, 2)),
(round((random() * 10 + 5)::numeric, 2)),
(round((random() * 10 + 5)::numeric, 2));
```

---

## 6. JSONB במקום קשר M:N

```sql
CREATE TABLE enrollments (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    courses JSONB
);

INSERT INTO enrollments (name, courses) VALUES
('Roni', '{
  "math": "2024-11-01",
  "history": "2024-11-15"
}'),
('Alon', '{
  "math": "2024-11-01"
}');
```