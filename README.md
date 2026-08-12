CREATE DATABASE IF NOT EXISTS StoreManagement;
USE StoreManagement;

DROP TABLE IF EXISTS Product;
DROP TABLE IF EXISTS Category;

CREATE TABLE Category (
    category_id INT PRIMARY KEY AUTO_INCREMENT,
    category_name VARCHAR(100) NOT NULL UNIQUE,
    description VARCHAR(255)
);

CREATE TABLE Product (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    product_name VARCHAR(150) NOT NULL,
    category_id INT NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL DEFAULT 0,
    
    FOREIGN KEY (category_id)
        REFERENCES Category(category_id)
        ON UPDATE CASCADE
        ON DELETE RESTRICT
);

INSERT INTO Category (category_name, description) VALUES
('Mobile Accessories', 'Accessories for mobile phones'),
('Kitchen', 'Kitchen tools and equipment'),
('Stationery', 'School and office supplies'),
('Footwear', 'Shoes and other footwear'),
('Toys', 'Toys and games for children');

INSERT INTO Product (product_name, category_id, price, stock) VALUES
('Phone Charger', 1, 450, 40),
('Power Bank', 1, 1200, 25),
('Non Stick Pan', 2, 850, 18),
('Water Bottle', 2, 350, 30),
('Notebook', 3, 120, 60),
('Pen Set', 3, 180, 50),
('Running Shoes', 4, 2200, 15),
('Sandals', 4, 750, 20),
('Toy Car', 5, 500, 25),
('Building Blocks', 5, 900, 12);

SELECT * FROM Category;
SELECT * FROM Product;


UPDATE Product
SET price = 500
WHERE product_id = 1;


DELETE FROM Product
WHERE product_id = 10;


SELECT
    c.category_name,
    p.product_name,
    p.price,
    p.stock
FROM Category c
JOIN Product p
ON c.category_id = p.category_id
ORDER BY c.category_name;
