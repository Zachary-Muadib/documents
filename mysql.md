# MySQL 语法速记大纲

#### 1. 数据定义语言 (DDL)
- **创建数据库**
  ```sql
  CREATE DATABASE IF NOT EXISTS database_name CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
  ```
- **修改数据库**
  ```sql
  ALTER DATABASE database_name CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
  ```
- **删除数据库**
  ```sql
  DROP DATABASE IF EXISTS database_name;
  ```
- **选择数据库**
  ```sql
  USE database_name;
  ```
- **创建表**
  ```sql
  CREATE TABLE IF NOT EXISTS table_name (column1 datatype [constraints], column2 datatype [constraints], ...);
  ```
- **修改表**
  - 添加列
    ```sql
    ALTER TABLE table_name ADD COLUMN new_column datatype;
    ```
  - 修改列
    ```sql
    ALTER TABLE table_name MODIFY COLUMN column_name new_datatype;
    ```
  - 删除列
    ```sql
    ALTER TABLE table_name DROP COLUMN column_name;
    ```
- **删除表**
  ```sql
  DROP TABLE IF EXISTS table_name;
  ```
- **重命名表**
  ```sql
  RENAME TABLE old_table_name TO new_table_name;
  ```
- **复制表结构**
  ```sql
  CREATE TABLE new_table LIKE old_table;
  ```
- **复制表（包括数据）**
  ```sql
  CREATE TABLE new_table AS SELECT * FROM old_table;
  ```
- **创建临时表**
  ```sql
  CREATE TEMPORARY TABLE temp_table_name (column1 datatype, ...);
  ```

#### 2. 数据类型
- **整型**：INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT
- **浮点型**：FLOAT, DOUBLE, DECIMAL
- **字符串**：CHAR, VARCHAR, TEXT, BLOB
- **日期时间**：DATE, DATETIME, TIMESTAMP, TIME, YEAR
- **位类型**：BIT
- **枚举**：ENUM('val1', 'val2', ...)
- **集合**：SET('val1', 'val2', ...)

#### 3. 索引和约束
- **创建索引**
  ```sql
  CREATE INDEX index_name ON table_name (column_name);
  ```
- **复合索引**
  ```sql
  CREATE INDEX index_name ON table_name (column1, column2, ...);
  ```
- **全文索引** (仅限于CHAR, VARCHAR, TEXT数据类型)
  ```sql
  CREATE FULLTEXT INDEX ft_index ON table_name (column_name);
  ```
- **空间索引** (用于地理空间数据)
  ```sql
  CREATE SPATIAL INDEX sp_index ON table_name (column_name);
  ```
- **删除索引**
  ```sql
  DROP INDEX index_name ON table_name;
  ```
- **主键**
  ```sql
  ALTER TABLE table_name ADD PRIMARY KEY (column_name);
  ```
- **外键**
  ```sql
  ALTER TABLE table_name ADD FOREIGN KEY (column_name) REFERENCES another_table (column_name);
  ```
- **唯一约束**
  ```sql
  ALTER TABLE table_name ADD UNIQUE (column_name);
  ```
- **检查约束** (MySQL 8.0.16及以上版本)
  ```sql
  ALTER TABLE table_name ADD CONSTRAINT constraint_name CHECK (condition);
  ```

#### 4. 数据操纵语言 (DML)
- **插入数据**
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, value2);
  ```
- **插入多条数据**
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, value2), (value3, value4), ...;
  ```
- **插入查询结果**
  ```sql
  INSERT INTO table_name (column1, column2) SELECT column1, column2 FROM another_table;
  ```
- **更新数据**
  ```sql
  UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
  ```
- **删除数据**
  ```sql
  DELETE FROM table_name WHERE condition;
  ```

#### 5. 基础查询语句
- **查询数据**
  ```sql
  SELECT column1, column2 FROM table_name;
  SELECT * FROM table_name;
  ```
- **条件筛选**
  ```sql
  SELECT * FROM table_name WHERE condition;
  ```
- **排序**
  ```sql
  SELECT * FROM table_name ORDER BY column ASC|DESC;
  ```
- **指定返回的记录数**
  ```sql
  SELECT * FROM table_name LIMIT number;
  ```
- **指定返回记录的偏移量**
  ```sql
  SELECT * FROM table_name LIMIT offset, number;
  ```
- **计算表中记录的数量**
  ```sql
  SELECT COUNT(*) FROM table_name;
  ```

#### 6. 数据聚合与分组
- **计数**
  ```sql
  SELECT COUNT(column_name) FROM table_name;
  ```
- **求和**
  ```sql
  SELECT SUM(column_name) FROM table_name;
  ```
- **平均**
  ```sql
  SELECT AVG(column_name) FROM table_name;
  ```
- **最大值/最小值**
  ```sql
  SELECT MAX(column_name) FROM table_name;
  SELECT MIN(column_name) FROM table_name;
  ```
- **分组**
  ```sql
  SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;
  ```
- **HAVING子句**
  ```sql
  SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name HAVING COUNT(*) > some_value;
  ```

#### 7. 高级查询
- **连接 (JOIN)**
  ```sql
  SELECT columns FROM table1 INNER|LEFT|RIGHT JOIN table2 ON table1.column = table2.column;
  ```
- **自连接**
  ```sql
  SELECT a.column_name, b.column_name FROM table_name a, table_name b WHERE a.common_field = b.common_field;
  ```
- **使用别名**
  ```sql
  SELECT column_name AS alias_name FROM table_name;
  ```
- **子查询**
  ```sql
  SELECT column_name FROM (SELECT column_name FROM table_name) AS subquery;
  ```
- **CASE语句**
  ```sql
  SELECT CASE WHEN condition THEN result1 ELSE result2 END FROM table_name;
  ```
- **联合查询 (UNION)**
  ```sql
  SELECT column_name FROM table1 UNION SELECT column_name FROM table2;
  ```

#### 8. 函数
- **字符串函数**：CONCAT(), LENGTH(), SUBSTRING(), UPPER(), LOWER(), REPLACE()
- **数值函数**：ROUND(), CEIL(), FLOOR(), ABS(), MOD()
- **日期和时间函数**：NOW(), CURDATE(), CURTIME(), DATE_ADD(), DATE_SUB(), DATEDIFF(), DATE_FORMAT()
- **条件函数**：IF(), CASE WHEN THEN ELSE END, COALESCE()
- **聚合函数**：GROUP_CONCAT()

#### 9. 视图
- **创建视图**
  ```sql
  CREATE VIEW view_name AS SELECT column_name FROM table_name WHERE condition;
  ```
- **修改视图**
  ```sql
  ALTER VIEW view_name AS SELECT column_name FROM table_name WHERE condition;
  ```
- **删除视图**
  ```sql
  DROP VIEW view_name;
  ```
- **查看视图**
  ```sql
  SHOW FULL TABLES IN database_name WHERE TABLE_TYPE LIKE 'VIEW';
  ```

#### 10. 事务处理
- **开始事务**
  ```sql
  START TRANSACTION;
  ```
- **提交**
  ```sql
  COMMIT;
  ```
- **回滚**
  ```sql
  ROLLBACK;
  ```
- **保存点**
  ```sql
  SAVEPOINT savepoint_name;
  ROLLBACK TO savepoint_name;
  ```
- **设置事务隔离级别**
  ```sql
  SET TRANSACTION ISOLATION LEVEL [ READ UNCOMMITTED | READ COMMITTED | REPEATABLE READ | SERIALIZABLE ];
  ```

#### 11. 用户和权限
- **创建用户**
  ```sql
  CREATE USER 'username'@'hostname' IDENTIFIED BY 'password';
  ```
- **修改用户密码**
  ```sql
  ALTER USER 'username'@'hostname' IDENTIFIED BY 'new_password';
  ```
- **删除用户**
  ```sql
  DROP USER 'username'@'hostname';
  ```
- **授予权限**
  ```sql
  GRANT privileges ON database.table TO 'username'@'hostname';
  ```
- **撤销权限**
  ```sql
  REVOKE privileges ON database.table FROM 'username'@'hostname';
  ```
- **查看权限**
  ```sql
  SHOW GRANTS FOR 'username'@'hostname';
  ```
- **查看当前用户**
  ```sql
  SELECT USER();
  ```
- **查看当前用户权限**
  ```sql
  SHOW GRANTS;
  ```

#### 12. 其他实用命令
- **查看当前数据库中的所有表**
  ```sql
  SHOW TABLES;
  ```
- **查看表结构**
  ```sql
  DESCRIBE table_name;
  ```
- **查看版本**
  ```sql
  SELECT VERSION();
  ```
- **查看当前正在执行的查询**
  ```sql
  SHOW PROCESSLIST;
  ```
- **锁定表**
  ```sql
  LOCK TABLES table_name READ|WRITE;
  ```
- **解锁表**
  ```sql
  UNLOCK TABLES;
  ```
- **导出查询结果为文件**
  ```sql
  SELECT column_name INTO OUTFILE 'file_name' FROM table_name;
  ```
- **执行SQL脚本文件**
  ```sql
  SOURCE file_name;
  ```
- **注释**
  - 单行注释：`-- 注释内容` 或 `# 注释内容`
  - 多行注释：`/* 注释内容 */`

#### 13. 性能优化
- **EXPLAIN**
  ```sql
  EXPLAIN SELECT * FROM table_name;
  ```
- **优化表**
  ```sql
  OPTIMIZE TABLE table_name;
  ```

#### 14. 高级主题
- **触发器**
  - 创建触发器
    ```sql
    CREATE TRIGGER trigger_name BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name FOR EACH ROW BEGIN ... END;
    ```
  - 删除触发器
    ```sql
    DROP TRIGGER trigger_name;
    ```
- **存储过程**
  - 创建存储过程
    ```sql
    CREATE PROCEDURE procedure_name(IN|OUT|INOUT param_name datatype) BEGIN ... END;
    ```
  - 调用存储过程
    ```sql
    CALL procedure_name(arguments);
    ```
  - 删除存储过程
    ```sql
    DROP PROCEDURE IF EXISTS procedure_name;
    ```
- **函数**
  - 创建函数
    ```sql
    CREATE FUNCTION function_name(returns_datatype) RETURNS datatype BEGIN ... END;
    ```
  - 删除函数
    ```sql
    DROP FUNCTION IF EXISTS function_name;
    ```
