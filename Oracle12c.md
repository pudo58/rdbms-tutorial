# Oracle Database 12c

## Function in Oracle 12c
- **NULLIF(param1,param2)**

> _nếu 2 tham số không bằng nhau,NULLIF sẽ trả về giá trị là tham số thứ 1_

> _NULLIF sẽ trả về null khi 2 tham số truyền vào bằng nhau_
```SQL
 SELECT NULLIF('tholv','t') FROM dual;

=> 'tholv'
 
 ```

- ### **CONCAT(param1,param2)**

> _CONCAT dùng để nối 2 chuỗi lại với nhau_
```SQL
SELECT CONCAT('tholv','nguyennt') FROM dual;
-- CHúng ta còn 1 kiểu nối chuỗi là dùng || 
SELECT 'tholv'||'nguyennt' FROM dual;

=> 'tholvnguyennt'
```
- ### **INSTR(string,SubString)**
 > _SubString trong thanm số là chuỗi con đưa vào để kiểm tra xem chuỗi con có nằm trong chuỗi string không , nếu có sẽ trả 
 về 
 số lần mà lặp lại_

 ```SQL
 SELECT INSTR('tholv','t') FROM dual;

 => 1
 ```
 - ### **LENGTH('param')**
 > _LENGTH trả về độ dài của chuỗi truyền vào_

 ```SQL
 SELECT LENGTH('nguyennt') FROM dual;

 => 8
 ```
 - ### **to_char(param)**
 > _to_char(param) ép kiểu dữ liệu về 1 chuỗi_
 ```SQL
 SELECT to_char(123) from dual;
 ```
- ### **Mệnh đề GROUP BY(column1,column2,...)**
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
- ### **Mệnh đề HAVING**
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

- ### **TRUNCATE TABLE table_name**
> _TRUNCATE TABLE dùng để xóa dữ liệu của 1 bảng , nhưng điểm đặc biệt ở đây khi xóa xong dữ liệu sẽ không thể phục hồi_

- ### **DELETE table_name** 
> _Dùng để xóa dữ liệu của 1 bảng, nhưng ta vẫn có thể khôi phục dữ liệu đó được. Khi xóa xong ta tiến hành ROLLBACK lại để lấy dữ liệu_
```SQL
DELETE Staff ;
ROLLBACK;
```
- ### **ROLLBACK,COMMIT**
> _ROLLBACK dùng để phục hồi lại dữ liệu của trước lúc thêm,sửa,xóa,update..._
> _COMMIT dùng để lưu những thay đổi vào db và khi ta đã commit thì không thể dùng rollback để phục hồi lại dữ liệu_
- ### **UNIQUE**
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
- ### **NULL**
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
- ### **JOIN ,INNER JOIN,LEFT JOIN,RIGHT JOIN**
> _Đều dùng để lấy dữ liệu từ nhiều bảng_
> _INNER JOIN dùng để lấy dữ liệu chung từ 2 bảng_
> _LEFT JOIN dùng để lấy dữ liệu phù hợp  từ bảng bên trái_
> _RIGHT JOIN dùng để lấy dữ liệu phù hợp  từ bảng bên phải_
```SQL
SELECT *FROM Staff f JOIN Admin a on f.admin_id = a.admin_id;
```
- ### **LIKE và = trong Oracle Database**
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
- ### **Lấy dữ liệu ngày giờ hiện tại**
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
- ### **CONSTRAINT(Ràng buộc)**
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
- ### **Truy vấn con(Sub Query)**
    - Truy vấn con (còn được gọi truy vấn phụ hay truy vấn lồng nhau) là một truy vấn bên trong truy vấn SQL khác và được nhúng bên trong mệnh đề WHERE. Một truy vấn con được sử dụng để trả về dữ liệu mà sẽ được sử dụng trong truy vấn chính như là một điều kiện để thu hẹp dữ liệu được thu nhận.
    - Truy vấn con sẽ trả về dữ liệu của 1 hoặc nhiều bảng , khi dùng join truy vấn con sẽ trả dữ liệu của nhiều bảng về
    ```SQL
    -- ví dụ :
    SELECT *FROM STAFF WHERE CREATED_DATE=(SELECT CREATED_DATE FROM DUAL WHERE ID = 1);

    -- VÍ DỤ :
    SELECT * FROM (SELECT ID,NAME FROM STAFF )WHERE ID=10;
    -- KHI NÀY THÌ TRUY VẤN CON SẼ TRẢ VỀ 1 BẢNG CÓ 2 CỘT GIÁ TRỊ VÀ DẤU SELECT * SẼ LẤY 2 GIÁ TRỊ TRONG TRUY VẤN CON ĐÓ. TRUY VẤN CON VIẾT NHIỀU SẼ QUEN .
    ```
- ### **DECLARE(Khai báo biến)**
    - Dùng để khai báo 1 hoặc nhiều biến trong Oracle Database
    - Cú pháp : 
    ```SQL
    DECLARE
        name VARCHAR2(255) ;
        age NUMBER(3);
    BEGIN                                  --- VIỆC LÀM SAU KHI KHAI BÁO BIẾN
        name:='tholv';                 -- gán giá trị bằng dấu ' := '
        age:=10;                       -- CHÚNG TA CÓ THỂ LÀM VIỆC THAO TÁC VỚI BIẾN 
        age:=age+10;
        DBMS_OUTPUT.PUT_LINE(name) ;
        DBMS_OUTPUT.PUT_LINE(age) ;
    END;                           -- KẾT THÚC
    ```
    - Lưu ý : _Khi chạy xong đoạn code trên thì chúng ta sẽ in được tên và tuổi, biến trong sql khi chạy xong sẽ không lưu vào db mà sẽ bị mất đi_

- ### **CREATE TYPE (Tạo 1 loại dữ liệu tự định nghĩa)**
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
- ### **TỪ KHÓA : UNION**
    - Toán tử UNION trả về giá trị của tất cả các hàng từ các câu lệnh truy vấn và xóa đi các phần tử bị trùng lặp.
    - Ví dụ
    ```SQL
    SELECT ID,NAME,AGE FROM STAFF INNER JOIN PRODUCT ON STAFF.ID = PRODUCT.ID WHERE STAFF_ID=116
    UNION 
    SELECT ID,NAME,AGE FROM STAFF INNER JOIN PRODUCT ON STAFF.ID = PRODUCT.ID WHERE STAFF_ID=87
    --- UNION  SẼ HỢP NHẤT DỮ LIỆU CỦA 2 CÂU TRUY VẤN THÀNH 1 KẾT QUẢ VÀ XÓA HẾT DỮ LIỆU BỊ TRÙNG CỦA 2 CÂU TRUY VẤN TRÊN
    --- CHÚNG TA CÓ THỂ TRUY VẤN BẰNG BẢNG KHÁC, KHÔNG NHẤT THIẾT PHẢI LÀ 2 BẢNG CÙNG TÊN , NHƯNG CÁC CỘT CỦA CÁC CÂU TRUY VẤN NÀY TRẢ VỀ KO CẦN CÙNG TÊN, CÙNG KIỂU DỮ LIỆU LÀ ĐƯỢC 
    ```
    - **TỪ KHÓA : UNION ALL**
    - Toán tử UNION ALL cũng giống với UNION nhưng UNION ALL không xóa các phần tử trùng lặp 
    - Ví dụ
    ```SQL
    SELECT ID,NAME,AGE FROM STAFF INNER JOIN PRODUCT ON STAFF.ID = PRODUCT.ID WHERE STAFF_ID=116
    UNION ALL 
    SELECT ID,NAME,AGE FROM STAFF INNER JOIN PRODUCT ON STAFF.ID = PRODUCT.ID WHERE STAFF_ID=87
    ```

- ### **Tạo bảng tạm, biến bảng bằng WITH**
    - WITH dùng để tạo một bảng tạm thời, 1 biến bảng. Bảng trên sẽ không tồn tại trong database khi ta chạy xong câu lệnh, Bảng tạm trên có thể thao tác dữ liệu được như bình thường . Dữ liệu của bảng tạm WITH sẽ phụ thuộc vào dữ liệu của các bảng khác.
    - Cú pháp :
    ```SQL
    WITH STAFF_COPY(ID,NAME,AGE) AS (
        SELECT ID,NAME,AGE FROM STAFF INNER JOIN PRODUCT ON STAFF.ID = PRODUCT.ID WHERE STAFF_ID=19
        UNION ALL 
        SELECT ID,NAME,AGE FROM STAFF INNER JOIN PRODUCT ON STAFF.ID = PRODUCT.ID WHERE STAFF_ID=116
     --- LÚC NÀY STAFF_COPY CHÍNH LÀ TÊN BẢNG VÀ ID,NAME,AGE LÀ TÊN CỘT CỦA BẢNG
     --- GIÁ TRỊ CỦA BẢNG CHÍNH LÀ KẾT QUẢ CỦA 2 CÂU LỆN TRUY VẤN TRÊN
    )SELECT * FROM STAFF_COPY WHERE AGE BETWEEN (SELECT AGE FROM STAFF WHERE ID=1) AND (SELECT AGE FROM STAFF WHERE ID=2);
    ```
- ### **Mệnh đề điều kiện IF - ELSE**
    - Cú pháp
    ```SQL
    DECLARE 
        A NUMBER(10);
        B NUMBER(10);
    BEGIN
        A:=10;
        B:=10;
    IF A==B THEN 
        DBMS_OUTPUT.PUT_LINE('A Equal B'); -- xuất ra màn hình
    ELSE IF A>B THEN
        DBMS_OUTPUT.PUT_LINE('A > B');
    ELSE 
        DBMS_OUTPUT.PUT_LINE('A < B ');     
    END IF;
    END ;
    ```
- ### **Vòng lặp FOR**
    - Vòng lặp for dùng để duyệt 1 mảng phần tử trong Database Oracle 
    - Vòng lặp for có 2 giá trị là item và array 
    - Cú pháp :
    ```SQL
    FOR item in array
    LOOP
    --- công việc cần làm
    END LOOP;
    --- item là biến chúng ta tự đặt như nào cũng được, còn array có thể là 1 mảng, 1 câu truy vấn con
    ```

    - Ví dụ 
    ```SQL
    --- xuất các số từ 1->10 
    BEGIN
    FOR X IN 1..10 LOOP 
        DBMS_OUTPUT.put_line(X); 
    END LOOP; 
    END;
    --- dùng for có select 

    FOR X IN (
        SELECT STAFF.ID_STAFF FROM STAFF JOIN PRODUCT ON PRODUCT.ID_STAFF = STAFF.ID_STAFF
                           JOIN CATEGORY ON CATEGORY.ID_CATEGORY = PRODUCT.ID_CATEGORY
    ) LOOP
    
    UPDATE PRODUCT SET ID_STAFF=X.ID_STAFF --- CÔNG VIỆC CỦA VÒNG LẶP
    -- X Ở ĐÂY CHÍNH LÀ BIẾN CỦA FOR 
    END LOOP;
    ```
- ### **Vòng lặp WHILE**
    - Vòng lặp while dùng để duyệt phần tử như for nhưng while sẽ ko biết trước điểm dừng
    - ví dụ
    ```SQL
    DECLARE 
        count NUMBER(10);
    BEGIN
        count:=10;
        WHILE count<20 LOOP  
            DBMS_OUTPUT.PUT_LINE(count) ;--- công việc của vòng lặp
            count:=count+1;
    END LOOP;
    END ;
    ```
- ### **Ví dụ về FOR LOOP**
    - Để hiểu rõ hơn về FOR LOOP thì mình xin lấy ví dụ sau:
        - Cho cấu trúc bảng sau :
            - TEACHER(***id_teacher***,name,age,gender,phone)
            - STUDENT(***id_student***,***id_teacher***,name,age,gender)            
            - Code 
            ```SQL
            CREATE TABLE TEACHER 
            (
                ID_TEACHER NUMBER(10) NOT NULL PRIMARY KEY,
                NAME NVARCHAR2(255 CHAR) NOT NULL,
                AGE NUMBER(3) NOT NULL,
                GENDER NVARCHAR2(8 CHAR) NOT NULL
            );
            CREATE TABLE STUDENT
            (
                ID_STUDENT NUMBER(10) NOT NULL PRIMARY KEY,
                ID_TEACHER NUMBER(10) NOT NULL,
                NAME NVARCHAR2(255 CHAR) NOT NULL,
                AGE NUMBER(3) NOT NULL,
                GENDER NVARCHAR2(8 CHAR) NOT NULL,
                PHONE NVARCHAR(15) NOT NULL,
                CONSTRAINT FK_STUDENT FOREIGN KEY (ID_TEACHER) REFERENCES TEACHER(ID_TEACHER);
            );
            CREATE SEQUENCE SEQ_TEACHER;
            CREATE SEQUENCE SEQ_STUDENT;
            INSERT INTO TEACHER VALUES(SEQ_TEACHER.NEXTVAL,'THOLV',25,'NAM');
            INSERT INTO TEACHER VALUES(SEQ_TEACHER.NEXTVAL,'HIEPTH',35,'NAM');
            INSERT INTO TEACHER VALUES(SEQ_TEACHER.NEXTVAL,'NHATLH',20,'NAM');
            INSERT INTO TEACHER VALUES(SEQ_TEACHER.NEXTVAL,'NGUYENNT',20,'NỮ');
            INSERT INTO TEACHER VALUES(SEQ_TEACHER.NEXTVAL,'HOANGTT',19,'NỮ');
            --------------------------------------------------------------------
            INSERT INTO STUDENT VALUES(SEQ_STUDENT.NEXTVAL,1,'HOANGNT',17,'NAM');
            INSERT INTO STUDENT VALUES(SEQ_STUDENT.NEXTVAL,1,'HOANT',17,'NỮ');
            INSERT INTO STUDENT VALUES(SEQ_STUDENT.NEXTVAL,1,'HAIVQ',17,'NAM');
            INSERT INTO STUDENT VALUES(SEQ_STUDENT.NEXTVAL,1,'HIVQ',17,'NỮ');
            INSERT INTO STUDENT VALUES(SEQ_STUDENT.NEXTVAL,2,'THUNN',17,'NỮ');
            --- ĐỀ BÀI : HÃY CHUYỂN TẤT CẢ HỌC SINH CỦA  THẦY GIÁO LÀ 'THOLV' SANG THẦY 'HIEPTH'
            --- Ý TƯỞNG : CHÚNG TA CÓ THỂ THẤY ĐƯỢC THẦY GIÁO 'THOLV' ĐANG CÓ 4 HỌC SINH (ID=1 LÀ THOLV)
                        -- TRONG TRƯỜNG HỢP CÓ 4 DỮ LIỆU NÀY TA PHẢI THỰC HIỆN UPDATE HÀNG LOẠT , LƯU GIÁ TRỊ CŨ VÀO 1 MẢNG BẰNG VÒNG LẶP FOR VÀ TIẾN HÀNH UPDATE HÀNG LOẠT
            -- LÀM :
            BEGIN 
            FOR X IN (
                SELECT * FROM STUDENT WHERE ID_TEACHER=1;
            )LOOP
            UPDATE STUDENT SET ID_TEACHER=2 WHERE ID_TEACHER=X.ID_TEACHER;
            END LOOP;
            END;
            ```
- ### **CASE WHEN(SWITCH CASE)**
    - CASE WHEN có cú pháp giống SWITCH CASE trong các ngôn ngữ lập trình như Java,C,C++,C#,Javascript ...
    - CASE WHEN có rất nhiều cách dùng, ở đây mình chỉ đemo 1 cách là dùng trong select .
    - Code demo CASE WHEN không cần truyền điều kiện vào CASE mà sẽ so sánh trực tiếp trong WHEN
    ```SQL
    SELECT T.ID_TEACHER , CASE  
                        WHEN T.AGE=20 THEN  'Trẻ'
                        WHEN T.AGE=19 THEN ' Qúa trẻ'
                        ELSE 'Bình thường'
                        END 
    FROM
    (
        SELECT * FROM TEACHER WHERE AGE <30
    ) T
    WHERE T.GENDER LIKE 'NAM';
    ```
    - Code demo CASE WHEN cơ bản
    ```SQL
    SELECT T.ID_TEACHER , CASE T.AGE 
                        WHEN 20 THEN  'Trẻ'
                        WHEN 19 THEN ' Qúa trẻ'
                        ELSE 'Bình thường'
                        END 
    FROM
    (
        SELECT * FROM TEACHER WHERE AGE <30
    ) T  --T là tên bảng của câu truy vấn con , đặt ntn cũng được
    WHERE T.GENDER LIKE 'NAM';
    ```
- ### **SELECT DISTINCT**
    - Từ khóa DISTINCT trong SELECT dùng để chọn ra những bản ghi không bị trùng lặp. DISTINCT sẽ so sánh từng bản ghi với nhau và sẽ loại bỏ kết quả trùng lặp. Nhưng ở dữ liệu lớn tầm vài chục vài trăm triệu bản ghi thì DISTINCT có vẻ chạy rất chậm và ăn nhiều tài nguyên của máy chủ. 
    - code demo :
    ```SQL
    SELECT DISTINCT 
        ID_TEACHER,NAME,AGE
    FROM TEACHER WHERE AGE<35 AND GENDER='NAM';
    ```
- ### **INITCAP(Xử lý chuỗi)**
    - INITCAP dùng để viết hoa các chữ cái đầu trong các từ của 1 chuỗi, các chữ cái không phải chữ cái đầu mà đang ở trạng thái viết hoa sẽ trở về viết thường
    - code :
    ```SQL
    SELECT NAME FROM TEACHER WHERE ID_TEACHER=1;
    --- Kết quả : THOLV LA VAN Tho
    --- sau khi dùng INITCAP
    SELECT INITCAP(NAME) FROM TEACHER WHERE ID_TEACHER=1;
    --- Kết quả : Tholv La Van Tho
    ```
- ### **UPPER , LOWER (Xử lý chuỗi)**
    - UPPER('paramString') dùng để viết hoa chuỗi truyền vào .

    - LOWER('paramString') dùng để viết thường chuỗi truyền vào
    ```SQL
    SELECT UPPER(NAME) FROM TEACHER WHERE AGE <30;
    --- SẼ NHÂN ĐC TÊN VIẾT HOA

    SELECT LOWER(NAME) FROM TEACHER WHERE AGE <30;
    --- SẼ NHẬN ĐƯỢC TÊN VIẾT THƯỜNG 
    ```
# PLSQL/Oracle Database
    
- ### **CREATE OR REPLACE VIEW**
    - VIEW  là 1 đoạn lệnh được lập trình viết sẵn trong Database , khi ta gọi VIEW thì nó sẽ hiển thị như
    
     bảng bình thường, có thể nói VIEW là bảng ảo.

    - Công dụng để hiển thị dữ liệu .

    - Code ví dụ : Tạo view từ dữ liệu của 1 bảng

    ```SQL
    CREATE OR REPLACE VIEW TeacherView AS
    SELECT * FROM TEACHER WHERE AGE <30;
    ```
    - Code ví dụ : Tạo view từ dữ liệu của nhiều bảng
    ```SQL
    CREATE OR REPLACE VIEW TeacherView AS
    SELECT * FROM TEACHER T JOIN STUDENT S
                        ON T.ID_TEACHER=S.ID_STUDENT;
    ```
    - Cách gọi VIEW : SELECT * FROM VIEW_NAME;
    ```SQL
    SELECT * FROM TearcherView;
    ```
    - ### **CREATE OR REPLACE TRIGGER**
        - TRIGGER là 1 hàm thuộc PLSQL  **_không có tham số đầu vào_**

        - TRIGGER sẽ được gọi khi người dùng tác động làm thay đổi dữ liệu như INSERT,DELETE,UPDATE.

        - Ưu điểm : có thể kiểm tra lỗi ở mức cơ sở dữ liệu,bảo vệ được tính toàn vẹn của dữ liệu.
        Bình thường các bạn sẽ kiểm tra lỗi trong phía frontend bằng js,kiểm tra lỗi trong phía backend bằng Java,C++,C#,Pyhon,Php...Còn TRIGGER sẽ kiểm tra lỗi ở mức của Cơ sở dữ liệu.

        - Lưu ý : _khi bạn viết câu lệnh INSERT,DELETE,UPDATE thì các TRIGGER bạn tạo ra nó sẽ tự động chạy ngầm_

        - Các loại TRIGGER : BEFORE TRIGGER,AFTER TRIGGER.
            - Mỗi loại sẽ có 3 trường hợp là BEFORE INSERT,UPDATE,DELETE VÀ AFTER INSERT,DELETE,UPDATE.
            - Ví dụ khi bạn viết BEFORE INSERT thì hàm này sẽ được gọi trước lúc bạn INSERT vào cơ sở dữ liệu,còn bạn viết AFTER DELETE thì hàm này sẽ được gọi vào sau lúc bạn DELETE vào cơ sở dữ liệu.
        - Trigger dùng để kiểm tra CONSTRAINT các khóa phụ để bảo toàn dữ liệu .

        - Demo code tạo Trigger BEFORE INSERT.

        - Ký hiệu <b>:NEW</b> là chỉ định đây là dữ liệu mới do người dùng insert vào table .
        - Ký hiệu <b>:OLD</b> là chỉ định đây là dữ liệu cũ của table . 
        ```SQL
        CREATE OR REPLACE TRIGGER BEFORE_INSERT_TEACHER
        BEFORE INSERT 
        ON TEACHER
        FOR EACH ROW
        DECLARE 
            ERROR_AGE EXCEPTION; -- khai báo ngoại lệ
        BEGIN
        --- CHECK DỮ LIỆU ĐẦU VÀO
        IF 
            :NEW.AGE <18 THEN
            RAISE ERROR_AGE; -- GÁN LỖI CHO EXCEPTION
        END IF;
        EXCEPTION
            WHEN ERROR_AGE THEN
            RAISE_APPLICATION_ERROR(-20001,'AGE IS NOT ENOUGH'); --- bắn lỗi ra console
            ROLLBACK; --TRÁNH LOG LẠI BẢNG , NÊN CHO VÀO
        
        END;
        ```
        - Chúng ta có thể tạo 1 TRIGGER đảm nhiệm BEFORE INSERT,DELETE,UPDATE.
        - Code demo :
         ```SQL
        CREATE OR REPLACE TRIGGER BEFORE_INSERT_TEACHER
        BEFORE INSERT OR UPDATE OR DELETE -- CHÚNG TA CÓ THỂ TÙY CHỈNH PHẦN NÀY 
        ON TEACHER
        FOR EACH ROW
        DECLARE 
            ERROR_AGE EXCEPTION; -- khai báo ngoại lệ
        BEGIN
        --- CHECK DỮ LIỆU ĐẦU VÀO
        IF 
            :NEW.AGE <18 THEN
            RAISE ERROR_AGE; -- GÁN LỖI CHO EXCEPTION
        END IF;
        EXCEPTION
            WHEN ERROR_AGE THEN   -- khi có lỗi
                RAISE_APPLICATION_ERROR(-20001,'AGE IS NOT ENOUGH'); --- ném ra lỗi 
                ROLLBACK; --TRÁNH LOG LẠI BẢNG , NÊN CHO VÀO       
        END;
        ```
        - Demo code TRIGGER AFTER INSERT,DELETE,UPDATE.
        ```SQL
        CREATE OR REPLACE TRIGGER AFTER_INSERT_TRIGGER
        AFTER INSERT 
        ON TEACHER
        FOR EACH ROW
        BEGIN 
            IF :NEW.NAME IS NULL OR :NEW.AGE < 19 THEN
                INSERT INTO TEACHER VALUES(SEQ_TEACHER.NEXTVAL,CONCAT(:NEW.NAME,'CANNOT BE NULL'),:NEW.AGE);
            END IF;
            
        END ;
        ```
    - ### **CREATE OR REPLACE FUNCTION**
        - FUNCTION là một hàm thực hiện một chức năng nào đó và sẽ phải trả về một giá trị duy nhất .
        - FUNCTION thường sẽ có tham số, và chia làm 3 loại tham số là IN,OUT,IN OUT .
            - IN : Tham số đầu vào,đây là loại chúng ta hay dùng nhất .
            - OUT : Tham số đầu ra.
            - IN OUT : Tham số đầu vừa vào vừa ra .
        - Cách tạo FUNCTION :
        ```SQL
        --- TẠO FUNCTION TÍNH TỔNG 2 SỐ 
        CREATE OR REPLACE FUNCTION SUM_NUMBER(NUMBER_1 NUMBER,NUMBER_2 NUMBER)
        RETURN NUMBER
        AS 
            RESULT NUMBER(10);
        BEGIN
            RESULT:=NUMBER_1+NUMBER_2;
            RETURN RESULT;
        END;

        ---- GỌI FUNCTION---- 
        DECLARE   
             n3 number(2); ---KHIA BÁO BIẾN    
        BEGIN   
            n3 := SUM_NUMBER(11,22);    ---SUM_NUMBER LÀ TÊN FUNCTION, CHÚNG TA CHỈ CẦN GHI TÊN LÀ CÓ THỂ CALL DC FUNCTION.
            dbms_output.put_line('SUM ' || n3);    
        END;
    - ### **CREATE OR REPLACE PROCEDURE**
        - PROCEDURE là một hàm con, chương trình con,PROCEDURE không trả về giá trị như FUNCTION, PROCEDURE chứa bên trong những câu lệnh PLSQL. 
        - Code demo :
        ```SQL
        CREATE OR REPLACE PROCEDURE PRINT_SAY_HELLO(message NVARCHAR2 )
        IS
        BEGIN
        DBMS_OUTPUT.PUT_LINE('HELLO '|| message);
        END ;
        ```
        - Gọi PROCEDURE 
        ```SQL
        --- CÁCH 1 :
        CALL PRINT_SAY_HELLO('NGUYENNT');
        --- CÁCH 2 :
        EXECUTE PRINT_SAY_HELLO('NGUYENNT');
        ```
        


            



    













