
[[SQL]]

DataType

Numeric DataType
Data And Time DataType
String DataType





-- How to enforce that Column doesn't have null ?
CREATE TABLE customers(
	id INT NOT NULL,
	name VARCHAR(100) NOT NULL



-- How to assign a Default Value to Column 
-- Is it wrong ?

CREATE TABLE employee2(
	name VARCHAR(100),
	acc_type VARCHAR(50) DEFAULT 'saving'
);


CREATE TABLE employee3(
	id INT NOT NULL,
	name VARCHAR(100) NOT NULL,
	acc_type VARCHAR(50) NOT NULL DEFAULT 'saving'
);
);





SELECT REPLACE ('Hello Buddy','Hello','Hey');
SELECT REVERSE ('Hello World');
SELECT UPPER ('Hello World');
SELECT LOWER ('Hello World');
SELECT UCASE ('Hello World');
SELECT LCASE ('Hello World');

SELECT CHAR_LENGTH('A man'); -- It Count Space as well

SELECT INSERT('Hello WhatsApp',6,0,'Aman');


SELECT LEFT('Hello World',3);
SELECT RIGHT('Hello World',3);
SELECT REPEAT('Hello',5);
SELECT TRIM('    Hello World    ');




CONCAT, CONCAT_WS
SUBSTRING(column,startIdx,endingIdx)