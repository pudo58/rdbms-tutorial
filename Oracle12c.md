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





