# Schéma de Base de Données - Système de Gestion de Bibliothèque Universitaire

## Tables Principales

### 1. Users (Utilisateurs)
```sql
CREATE TABLE Users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id VARCHAR(20) UNIQUE, -- Pour les étudiants
    staff_id VARCHAR(20) UNIQUE,   -- Pour le personnel
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(15),
    user_type ENUM('student', 'faculty', 'staff', 'admin') NOT NULL,
    department_id INT,
    registration_date DATE NOT NULL,
    status ENUM('active', 'suspended', 'graduated') DEFAULT 'active',
    max_books_allowed INT DEFAULT 5,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### 2. Books (Livres)
```sql
CREATE TABLE Books (
    book_id INT PRIMARY KEY AUTO_INCREMENT,
    isbn VARCHAR(20) UNIQUE,
    title VARCHAR(200) NOT NULL,
    subtitle VARCHAR(200),
    author VARCHAR(200) NOT NULL,
    publisher VARCHAR(100),
    publication_year YEAR,
    edition VARCHAR(50),
    language VARCHAR(30) DEFAULT 'French',
    pages INT,
    category_id INT,
    location_shelf VARCHAR(20),
    total_copies INT DEFAULT 1,
    available_copies INT DEFAULT 1,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### 3. Categories (Catégories)
```sql
CREATE TABLE Categories (
    category_id INT PRIMARY KEY AUTO_INCREMENT,
    category_name VARCHAR(100) NOT NULL,
    category_code VARCHAR(10) UNIQUE,
    description TEXT,
    parent_category_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 4. Borrowings (Emprunts)
```sql
CREATE TABLE Borrowings (
    borrowing_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    book_id INT NOT NULL,
    borrow_date DATE NOT NULL,
    due_date DATE NOT NULL,
    return_date DATE,
    status ENUM('active', 'returned', 'overdue', 'lost') DEFAULT 'active',
    renewal_count INT DEFAULT 0,
    fine_amount DECIMAL(10,2) DEFAULT 0.00,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### 5. Reservations (Réservations)
```sql
CREATE TABLE Reservations (
    reservation_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT NOT NULL,
    book_id INT NOT NULL,
    reservation_date DATE NOT NULL,
    expiry_date DATE NOT NULL,
    status ENUM('active', 'fulfilled', 'cancelled', 'expired') DEFAULT 'active',
    priority_level INT DEFAULT 1,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### 6. Departments (Départements)
```sql
CREATE TABLE Departments (
    department_id INT PRIMARY KEY AUTO_INCREMENT,
    department_name VARCHAR(100) NOT NULL,
    department_code VARCHAR(10) UNIQUE,
    faculty VARCHAR(100),
    head_of_department VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 7. Fines (Amendes)
```sql
CREATE TABLE Fines (
    fine_id INT PRIMARY KEY AUTO_INCREMENT,
    borrowing_id INT NOT NULL,
    user_id INT NOT NULL,
    fine_type ENUM('overdue', 'damage', 'lost') NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    description TEXT,
    issued_date DATE NOT NULL,
    paid_date DATE,
    status ENUM('pending', 'paid', 'waived') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Relations et Contraintes

```sql
-- Relations Foreign Keys
ALTER TABLE Users ADD FOREIGN KEY (department_id) REFERENCES Departments(department_id);
ALTER TABLE Books ADD FOREIGN KEY (category_id) REFERENCES Categories(category_id);
ALTER TABLE Categories ADD FOREIGN KEY (parent_category_id) REFERENCES Categories(category_id);
ALTER TABLE Borrowings ADD FOREIGN KEY (user_id) REFERENCES Users(user_id);
ALTER TABLE Borrowings ADD FOREIGN KEY (book_id) REFERENCES Books(book_id);
ALTER TABLE Reservations ADD FOREIGN KEY (user_id) REFERENCES Users(user_id);
ALTER TABLE Reservations ADD FOREIGN KEY (book_id) REFERENCES Books(book_id);
ALTER TABLE Fines ADD FOREIGN KEY (borrowing_id) REFERENCES Borrowings(borrowing_id);
ALTER TABLE Fines ADD FOREIGN KEY (user_id) REFERENCES Users(user_id);
```

## Index pour Performance

```sql
-- Index pour améliorer les performances
CREATE INDEX idx_users_email ON Users(email);
CREATE INDEX idx_users_student_id ON Users(student_id);
CREATE INDEX idx_books_isbn ON Books(isbn);
CREATE INDEX idx_books_title ON Books(title);
CREATE INDEX idx_borrowings_user_status ON Borrowings(user_id, status);
CREATE INDEX idx_borrowings_due_date ON Borrowings(due_date);
CREATE INDEX idx_reservations_user_status ON Reservations(user_id, status);
```