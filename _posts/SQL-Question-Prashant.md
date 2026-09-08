
[[SQL]]

- https://www.youtube.com/playlist?list=PLGf6Ram2AQh2GpckMjstVH6AaTm0kPfgI



# 1-20
INSERT INTO department(dept_name) VALUES("home");
ALTER TABLE department ADD COLUMN email VARCHAR(100);
UPDATE department SET email = "lazy@gmail.com" WHERE dept_id=4;
DELETE FROM department WHERE dept_id=3; 

# 21-41
CONCAT
GROUPCONCAT
SELECT GROUP_CONCAT(
	CONCAT(dept_id, ' - ', dept_name, '-',email)
	SEPARATOR  ' | '  
)
FROM department; 

-- IF a column Contains Null What will happen then, Will it be added ?
-- Too Handle NULL  (IF_NULl )


SELECT GROUP_CONCAT(CONCAT(dept_id,' - ',dept_name,' - ', IFNULL(email,'NULL'))
SEPARATOR '|'
) FROM department;



# 42-52
# 53-60
# 61-73
# 74-83