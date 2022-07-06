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
- **Lấy dữ liệu ngày giờ hiện tại**
    - CURRENT_DATE (Lấy dữ liệu ngày hiện tại)
    ```SQL
    SELECT * FROM STAFF WHERE CREATED_DATE =CURRENT_DATE;
    ```
    
    - CURRENT_TIMESTAMP (Lấy dữ liệu ngày giờ khu vực hiện tại)
     ```SQL
    SELECT CURRENT_TIMESTAMP FROM DUAL;
    ```
    
    - SYSDATE (Lấy dữ liệu ngày hiện tại của máy chủ)
     ```SQL
    SELECT SYSDATE FROM DUAL;
    ```
- **CONSTRAINT(Ràng buộc)**
    - NOT NULL (Ràng buộc không được để trống)
    ```SQL
    /* CÚ PHÁP : ALTER TABLE TABLE_NAME
                 MODIFY (COLUMN NOT NULL)
    */
    ALTER TABLE STAFF
    MODIFY (NAME NOT NULL);

    ```

         Lưu ý : Khi chúng ta thêm ràng buộc NOT NULL thì các dữ liệu trong DATABASE có sẵn không được phép null, nếu null chúng ta phải delete dữ liệu .
    - DEFAULT (Cung cấp giá trị mặc định cho 1 cột trong trường dữ liệu)
    ```SQL
    CREATE TABLE STAFF
    (
        ID_STAFF NUMBER(10) NOT NULL PRIMARY KEY,
        NAME VARCHAR(255) NOT NULL,
        ADDRESS VARCHAR(255) NOT NULL,
        STATUS NUMBER(1) DEFAULT 0
    );
    ```
        Lưu ý : Khi ta tạo bảng có từ khóa là DEFAULT thì khi INSERT dữ liệu nếu ta không INSERT cột STATUS thì nó mặc định dữ liệu là 0. Với các cột dữ liệu bằng VARCHAR các bạn có thể để như sau : NAME VARCHAR(255) DEFAULT 'tholv' .
    - UNIQUE (Ràng buộc 1 cột có giá trị là duy nhất trong bảng . Tất cả dữ liệu của cột có UNIQUE trong bảng sẽ không bị trùng lặp)
    ```SQL
    --- tạo UNIQUE khi CREATE TABLE 
    CREATE TABLE STAFF
    (
        ID_STAFF NUMBER(10) NOT NULL PRIMARY KEY,
        NAME VARCHAR(255) NOT NULL,
        ADDRESS VARCHAR(255) NOT NULL,
        EMAIL VARCHAR(255)UNIQUE NOT NULL 
    );
    --- tạo bằng ALTER TABLE khi đã có sẵn bảng
    ALTER TABLE STAFF
    ADD CONSTRAINT UNI_EMAIL UNIQUE (EMAIL);
    -- UNI_EMAIL là tên của ràng buộc(constraints) và đặt tên chúng theo cú pháp UNI_COLUMN, chúng ta có thể xóa ràng buộc UNIQUE bằng câu lệnh sau :
    DROP CONSTRAINT UNI_EMAIL;
    ```
    - PRIMARY KEY (Ràng buộc 1 trường là khóa chính)

        - Khi 1 cột được định nghĩa là khóa chính thì nó sẽ không được phép để null và không được phép trùng lặp. Nó sẽ là giá trị duy nhất trong 1 bảng . Thông thường khóa chính dùng để xác định 1 đối tượng, 
        chúng ta sẽ thường làm việc với khóa chính và khóa phụ nhiều hơn .
        - Ràng buộc Khóa chính (PRIMARY KEY) khác với UNIQUE ở điểm là 1 bảng chỉ có thể có 1 khóa chính , nhưng 1 bảng có thể có rất nhiều cột có từ khóa UNIQUE.
        ```SQL 
        -- TẠO KHÓA CHÍNH KHI TẠO BẢNG
        CREATE TABLE STAFF
        (
            ID_STAFF NUMBER(10) NOT NULL PRIMARY KEY,
            NAME_STAFF VARCHAR(255) NOT NULL,
            ADDRESS VARCHAR(255) NOT NULL
        );
        --- NẾU BẢNG KHÔNG CÓ KHÓA CHÍNH TẠO BẰNG ALTER TABLE
        ALTER TABLE STAFF
        ADD CONSTRAINT PK_STAFF PRIMARY KEY (ID_STAFF);
        ```
    - FOREIGN KEY (Ràng buộc 1 trường là  khóa ngoại)    

        - Dùng để thiết lập khóa ngoại trên bảng, tham chiếu đến bảng khác thông qua giá trị của cột được liên kết. Giá trị của cột được liên kết phải là duy nhất trong bảng kia.
        - Giá trị duy nhất phải có ràng buộc PRIMARY KEY hoặc UNIQUE.
        - 1 bảng có thể có rất nhiều khóa ngoại
- **Truy vấn con(Sub Query)**
    - Truy vấn con (còn được gọi truy vấn phụ hay truy vấn lồng nhau) là một truy vấn bên trong truy vấn SQL khác và được nhúng bên trong mệnh đề WHERE. Một truy vấn con được sử dụng để trả về dữ liệu mà sẽ được sử dụng trong truy vấn chính như là một điều kiện để thu hẹp dữ liệu được thu nhận.
    - Truy vấn con sẽ trả về dữ liệu của 1 hoặc nhiều bảng , khi dùng join truy vấn con sẽ trả dữ liệu của nhiều bảng về
    ```SQL
    -- ví dụ :
    SELECT *FROM STAFF WHERE CREATED_DATE=(SELECT CREATED_DATE FROM DUAL WHERE ID = 1);

    -- VÍ DỤ :
    SELECT * FROM (SELECT ID,NAME FROM STAFF )WHERE ID=10;
    -- KHI NÀY THÌ TRUY VẤN CON SẼ TRẢ VỀ 1 BẢNG CÓ 2 CỘT GIÁ TRỊ VÀ DẤU SELECT * SẼ LẤY 2 GIÁ TRỊ TRONG TRUY VẤN CON ĐÓ. TRUY VẤN CON VIẾT NHIỀU SẼ QUEN .
    ```
- **DECLARE(Khai báo biến)**
    - Dùng để khai báo 1 hoặc nhiều biến trong Oracle Database
    - Cú pháp : 
    ```SQL
    DECLARE
    name VARCHAR2(255) ;
    age NUMBER(3);
    BEGIN
                                   --- VIỆC LÀM SAU KHI KHAI BÁO BIẾN
    name:='tholv';                 -- gán giá trị bằng dấu ' := '
    age:=10;                       -- CHÚNG TA CÓ THỂ LÀM VIỆC THAO TÁC VỚI BIẾN 
    age:=age+10;
    DBMS_OUTPUT.PUT_LINE(name) ;
    DBMS_OUTPUT.PUT_LINE(age) ;
    END;                           -- KẾT THÚC
    ```
    - Lưu ý : _Khi chạy xong đoạn code trên thì chúng ta sẽ in được tên và tuổi, biến trong sql khi chạy xong sẽ không lưu vào db mà sẽ bị mất đi_

- **CREATE TYPE (Tạo 1 loại dữ liệu tự định nghĩa)**
    - Dùng để tạo 1 loại dữ liệu tự định nghĩa, thường là OBJECT
    - Cú pháp :
    ```SQL

    --- create type
    CREATE TYPE STUDENT AS OBJECT
    (
        ID_STUDENT NUMBER(10),
        NAME NVARCHAR2(255)
        --- STUDENT ĐƯỢC TÍNH LÀ 1 KIỂU DỮ LIỆU , VÀ KIỂU DỮ LIỆU NÀY KO CÓ KHÓA CHÍNH VÀ CÁC RÀNG BUỘC 
    );

    --- Tạo bảng
    CREATE TABLE CLASS 
    (
        ID_CLASS NUMBER(10) NOT NULL PRIMARY KEY,
        STUDENT_CLASS STUDENT NOT NULL,-- ĐÂY LÀ KIỂU DỮ LIỆU STUDENT VỪA TẠO
        STATUS NUMBER(1) NOT NULL
    );
    --- THÊM BẢN GHI NHƯ SAU
    INSERT INTO CLASS VALUES (1,STUDENT(1,'tholv'),0);
    --- chúng ta thêm cột student thì phải bắt đầu bằng từ khóa student thì Oracle Database mới hiểu .
    --- 1 và tholv tương ứng là ID_STUDENT và NAME trong STUDENT
    --- truy vấn dữ liệu của bảng 
    SELECT * FROM CLASS ;
    -- NHƯNG KHI TRUY VẤN TA KHÔNG THỂ NHẬN ĐƯỢC GIÁ TRỊ CỤ THỂ CỦA STUDENT , TA CẦN TRUY VẤN NHƯ SAU 
    SELECT ID_CLASS,TREAT(STUDENT_CLASS AS STUDENT).NAME,STATUS FROM CLASS
    ```
    - Lưu ý : _TREAT(STUDENT_CLASS AS STUDENT).NAME thì STUDENT_CLASS chính là tên cột trong bảng, STUDENT là tên đối tượng TYPE STUDENT mà chúng ta tạo, NAME là thuộc tính của STUDENT_

- **Tạo bảng tạm, biến bảng bằng WITH**





            







