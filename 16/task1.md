Q1.96年に3回以上注文した（Ordersが3つ以上紐づいている）Customerのidと、注文回数  
A1.  
SELECT CustomerID FROM Orders WHERE OrderDate BETWEEN '1996-01-01' AND '1996-12-31' GROUP BY CustomerID HAVING COUNT(CustomerID) > 2 ORDER BY CustomerID ASC;  

Q2.過去、最も多くのOrderDetailが紐づいたOrderを取得してください。何個OrderDetailが紐づいていたでしょうか？  
A2.
SELECT s.OrderID, MAX(OrderDetailCount) FROM Orders AS s LEFT OUTER JOIN (SELECT COUNT(*) AS OrderDetailCount, OrderID FROM OrderDetails GROUP BY OrderID) AS o ON s.OrderID = o.OrderID ORDER BY OrderDetailCount DESC;  

Q3.Order数が多い順番にShipperのidを並べてください。Order数も表示してください  
A3.  
SELECT s.ShipperID, ShippingCount 
FROM Shippers AS s LEFT OUTER JOIN 
(SELECT COUNT(*) AS ShippingCount, ShipperID FROM Orders GROUP BY ShipperID) AS o 
ON s.ShipperID = o.ShipperID ORDER BY ShippingCount DESC;  

Q4.売上が高い順番にCountryを並べてください。売上も表示してください  
A4.  
SELECT ROUND(SUM(sales)) AS sales, c.Country FROM Orders AS o JOIN Customers AS c ON c.CustomerID = o.CustomerID JOIN (SELECT *, (od.Quantity * p.Price) AS sales FROM OrderDetails AS od JOIN Products AS p ON od.ProductID = p.ProductID) AS po ON po.OrderID = o.OrderID GROUP BY c.Country ORDER BY sales DESC;

Q5.国ごとの売上を年ごとに集計する  
A5.  
SELECT ROUND(SUM(sales)) AS sales, SUBSTR(o.OrderDate,0,5) AS OrderYear, c.Country FROM Orders AS o JOIN Customers AS c ON c.CustomerID = o.CustomerID JOIN (SELECT *, (od.Quantity * p.Price) AS sales FROM OrderDetails AS od JOIN Products AS p ON od.ProductID = p.ProductID) AS po ON po.OrderID = o.OrderID GROUP BY OrderYear, c.Country ORDER BY c.Country ASC;

Q6.Employeeテーブルに「Junior（若手）」カラム（boolean）を追加  
A6.  
ALTER TABLE Employees ADD COLUMN Junior boolean Default NULL;  
UPDATE Employees SET Junior = CASE
WHEN BirthDate > '1960-01-01' THEN 1
ELSE 0
END;  

Q7.Shipperにlong_relationカラム（boolean）を追加  
A7.
ALTER TABLE Shippers ADD COLUMN long_relation boolean Default NULL;

UPDATE Shippers AS s
SET long_relation =
CASE
WHEN ShippingCount >= 70 THEN 1
ELSE 0
END
FROM
(SELECT COUNT(*) AS ShippingCount, ShipperID FROM Orders GROUP BY ShipperID) AS o
WHERE s.ShipperID = o.ShipperID AND ShippingCount >= 70;

Q8.それぞれのEmployeeが最後に担当したOrderと、その日付  

SELECT MAX(o.OrderDate), e.EmployeeID
FROM Employees AS e
JOIN Orders AS o
ON e.EmployeeID = o.EMployeeID
GROUP BY e.EmployeeID ORDER BY o.EmployeeID ASC;

Q9.NULLの扱いに慣れる  
UPDATE Customers SET CustomerName = null where CustomerID = 1;
// nullはなし
SELECT * FROM Customers WHERE CustomerName IS NOT NULL;
// nullのみ
SELECT * FROM Customers WHERE CustomerName IS NULL;

Q10.JOINの扱いになれる
DELETE FROM Employees WHERE EmployeeID = 1;

// 削除したデータはなし
SELECT o.OrderID, o.CustomerID, e.EmployeeId, o.OrderDate
FROM Orders AS o
INNER JOIN Employees AS e ON e.EmployeeID = o.EmployeeID
ORDER BY e.EmployeeID; 


// 削除されたデータはnullで埋まる
SELECT o.OrderID, o.CustomerID, e.EmployeeId, o.OrderDate
FROM Orders AS o
LEFT OUTER JOIN Employees AS e ON e.EmployeeID = o.EmployeeID
WHERE o.EmployeeID = 1
ORDER BY e.EmployeeID; 
