# Oracle Database 12c

## Function in Oracle 12c
- **NULLIF(param1,param2)**

> _nếu 2 tham số không bằng nhau,NULLIF sẽ trả về giá trị là tham số thứ 1_

> _NULLIF sẽ trả về null khi 2 tham số truyền vào bằng nhau_
```SQL
 SELECT NULLIF('tholv','t') FROM dual;

=> 'tholv'
 
 ```

- **CONCAT(param1,param2)**

> _CONCAT dùng để nối 2 chuỗi lại với nhau_
```SQL
SELECT CONCAT('tholv','nguyennt') FROM dual;

=> 'tholvnguyennt'
```
- **INSTR(string,SubString)**
 > _SubString trong thanm số là chuỗi con đưa vào để kiểm tra xem chuỗi con có nằm trong chuỗi string không , nếu có sẽ trả 
 về 
 số lần mà lặp lại_

 ```SQL
 SELECT INSTR('tholv','t') FROM dual;

 => 1
 ```
 - **LENGTH('param')**
 > _LENGTH trả về độ dài của chuỗi truyền vào_

 ```SQL
 SELECT LENGTH('nguyennt') FROM dual;

 => 8
 ```
 - **to_char(param)**
 > _to_char(param) ép kiểu dữ liệu về 1 chuỗi_
 ```SQL
 SELECT to_char(123) from dual;
 ```
- **Mệnh đề GROUP BY(column1,column2,...)**
> Mệnh đề GROUP BY(column1,column2,...) sẽ nhóm các cột có cùng giá trị lại thành một 

> SELECT không group by
```SQL
SELECT name,age,gender FROM Staff;
```
|name|age|gender|
|----|---|------|
|tholv|20|Nam|
|tholv|20|Nam|
|Nguyennt|18|Nu|

> SELECT có group by
```SQL
SELECT name,age,gender FROM Staff GROUP BY name,age,gender;
```
|name|age|gender|
|----|---|------|
|tholv|20|Nam|
|Nguyennt|18|Nu|
- **Mệnh đề HAVING**
> _Mệnh đề HAVING được sử dụng cùng lúc và đứng sau GROUP BY để chỉ ra điều kiện để nhóm các cột có cùng giá trị_

> SELECT không HAVING
```SQL
SELECT name,age,gender FROM Staff GROUP BY name,age,gender;
```
|name|age|gender|
|----|---|------|
|tholv|20|Nam|
|Nguyennt|18|Nu|

> SELECT **có** HAVING
```SQL
SELECT name,age,gender FROM Staff GROUP BY name,age,gender HAVING age<19;
```
|name|age|gender|
|----|---|------|
|Nguyennt|18|Nu|

- **TRUNCATE TABLE table_name**
> _TRUNCATE TABLE dùng để xóa dữ liệu của 1 bảng , nhưng điểm đặc biệt ở đây khi xóa xong dữ liệu sẽ không thể phục hồi_

- **DELETE table_name** 
> _Dùng để xóa dữ liệu của 1 bảng, nhưng ta vẫn có thể khôi phục dữ liệu đó được. Khi xóa xong ta tiến hành ROLLBACK lại để lấy dữ liệu_
```SQL
DELETE Staff ;
ROLLBACK;
```
- **ROLLBACK,COMMIT**
> _ROLLBACK dùng để phục hồi lại dữ liệu của trước lúc thêm,sửa,xóa,update..._
> _COMMIT dùng để lưu những thay đổi vào db và khi ta đã commit thì không thể dùng rollback để phục hồi lại dữ liệu_
- **UNIQUE**
> _Đây là từ khóa chỉ 1 trường là duy nhất trong bảng_ 
```SQL
CREATE TABLE STAFF
(
    ID_STAFF NUMBER(10) NOT NULL,
    NAME_STAFF VARCHAR2(255) NOT NULL,
    PHONE NUMBER(10) NOT NULL UNIQUE,
    PRIMARY KEY(ID_STAFF) 
);
```
- **NULL**
> _Đây là từ khóa để chỉ định 1 trường hoặc 1 cột là TRỐNG, Trong OracleDataBase thì ký tự trống '' cũng là NULL_
> Chúng ta không thể so sánh 2 trường = null , ví dụ : name=null , chúng ta dùng is null hoặc is not null để so sánh
```SQL
INSERT INTO STAFF(NAME,AGE) VALUES('',19);
> ERROR 
INSERT INTO STAFF(NAME,AGE) VALUES(NULL,19);
> ERROR
INSERT INTO STAFF(NAME,AGE) VALUES('THOLV',19);
> NOT ERROR
```
- **JOIN ,INNER JOIN,LEFT JOIN,RIGHT JOIN**
> _Đều dùng để lấy dữ liệu từ nhiều bảng_
> _INNER JOIN dùng để lấy dữ liệu chung từ 2 bảng_
> _LEFT JOIN dùng để lấy dữ liệu phù hợp  từ bảng bên trái_
> _RIGHT JOIN dùng để lấy dữ liệu phù hợp  từ bảng bên phải_
```SQL
SELECT *FROM Staff f JOIN Admin a on f.admin_id = a.admin_id;
```
- **LIKE và = trong Oracle Database**
> _Dấu '=' dùng để so sánh 2 giá trị có bằng nhau hay không, còn like thì cũng tương tự nhưng like có thể dùng để so sánh gần đúng hoặc conatain,startwith,endwith,... Trường hợp so sánh này thì like nhỉnh hơn '='.
```SQL
-- dùng =
SELECT name,age,gender FROM Staff WHERE name = 'tholv';
```
|name|age|gender|
|----|---|------|
|tholv|20|Nam|

```SQL
-- DÙNG LIKE 
SELECT name,age,gender FROM Staff WHERE name LIKE '%t%';
```
|name|age|gender|
|----|---|------|
|tholv|20|Nam|







