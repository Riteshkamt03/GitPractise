Creating a stored procedure with one parameter

The following query returns a product list from the products table in the sample database:

SELECT
    product_name,
    list_price
FROM 
    production.products
ORDER BY
    list_price;
Code language: SQL (Structured Query Language) (sql)

You can create a stored procedure that wraps this query using the CREATE PROCEDURE statement:

CREATE PROCEDURE uspFindProducts
AS
BEGIN
    SELECT
        product_name,
        list_price
    FROM 
        production.products
    ORDER BY
        list_price;
END;
Code language: SQL (Structured Query Language) (sql)

However, this time we can add a parameter to the stored procedure to find the products whose list prices are greater than an input price:

ALTER PROCEDURE uspFindProducts(@min_list_price AS DECIMAL)
AS
BEGIN
    SELECT
        product_name,
        list_price
    FROM 
        production.products
    WHERE
        list_price >= @min_list_price
    ORDER BY
        list_price;
END;
Code language: SQL (Structured Query Language) (sql)

In this example:

    First, we added a parameter named @min_list_price to the uspFindProducts stored procedure. Every parameter must start with the @ sign. The AS DECIMAL keywords specify the data type of the @min_list_price parameter. The parameter must be surrounded by the opening and closing brackets.
    Second, we used @min_list_price parameter in the WHERE clause of the SELECT statement to filter only the products whose list prices are greater than or equal to the @min_list_price.