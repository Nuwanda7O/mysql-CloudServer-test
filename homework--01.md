# homework--01

```mysql
DROP TABLE Student;
DROP TABLE Score;
DROP TABLE Course;
#[2] 在数据库Studentdb中使用DDL语句创建学生表Student
CREATE TABLE Student(
	Sno CHAR(4) PRIMARY KEY,
	Sname VARCHAR(8) NOT NULL,
	Gender CHAR(2),
	Birthday date,
	Haddress VARCHAR(50),
	Height DECIMAL(3,2),
	Remark TINYTEXT
);
#[3] 在数据库Studentdb中使用DDL语句创建课程表Course
CREATE TABLE Course(
	Cno CHAR(4) PRIMARY KEY,
	Cname VARCHAR(20) NOT NULL,
	Credit INT NULL
);
#[4] 在数据库Studentdb中使用DDL语句创建成绩表Score
CREATE TABLE Score(
	Sno CHAR(4),
	Cno CHAR(4),
	Grade DECIMAL(3,1) DEFAULT(NULL),
	PRIMARY KEY(Sno,Cno)
);
#[5] 将下列数据插入Student表中
INSERT INTO Student
VALUES
	('0001','刘一平','男','1990-10-1','温州市环城西路201号','1.78',NULL),
	('0002','张得民','男','1990-12-2','杭州市下沙路22号','1.65',NULL),
	('0003','马东','男','1990-7-4','宁波市中山北道20号','1.71',NULL),
	('0004','肖海燕','女','1990-3-15','温州市越秀北路43号','1.65',NULL),
	('0005','张民华','女','1991-5-13','宁波市艮山路7号','1.63',NULL);
#[6] 将下列数据插入Student表中
INSERT INTO Course VALUES ('0001','计算机基础',2)
INSERT INTO Course VALUES ('0002','管理学原理',3)
INSERT INTO Course VALUES ('0003','数据库原理及应用',3)
INSERT INTO Course VALUES ('0004','项目管理',2)
INSERT INTO Course VALUES ('0005','毕业论文',10)
#[7] 将下列数据插入Student表中
INSERT INTO Score VALUES
('0001','0001', 80.0),
('0001','0002', 90.0),
('0001','0003', 70.0),
('0001','0004', 85.0),
('0001','0005', 92.0),
('0002','0001', 78.0),
('0002','0002', NULL),
('0002','0003', 77.0),
('0002','0004', 67.0),
('0003','0001', 66.0),
('0003','0002', 76.0),
('0003','0003', NULL),
('0003','0004', 73.0)
#[8] 查询全体学生的详细记录(不包括选课信息)
SELECT * FROM Student
#[9] 查询学生表中学生的姓名和地址信息
SELECT Sname,Haddress FROM Student
#[10]查询学生表中“刘”姓学生的信息
SELECT * FROM Student WHERE Sname LIKE '刘%'
#[11]查询学生表中姓名包含“民”的学生的信息
SELECT * FROM Student WHERE Sname LIKE '%民%'
#[12]查询所有身高1.75以上的男学生的学号和姓名
SELECT Sno,Sname FROM Student WHERE Height>1.75
#[13]查询所有来自“宁波”的学生姓名、性别和年龄
SELECT Sname,Gender,ROUND(DATEDIFF(CURRENT_DATE(),Birthday)/365) AS 'Age'
FROM Student
WHERE Haddress LIKE '宁波%'
#[14]查询没有考试成绩的学生学号和课程编号
SELECT sno,cno
FROM score
WHERE Grade IS NULL
#[15]查询所有参加过考试的学生学号
SELECT DISTINCT sno
FROM score
WHERE Grade IS NOT NULL
#[16]查询所有学分不小于3的课程名
SELECT Cname
FROM course
WHERE credit>=3
#[17]查询学分在1~5范围内的课程编号和课程名称
SELECT Cno,Cname
FROM course
WHERE credit BETWEEN 1 AND 5
#[18]查询“数据库原理及应用”课程的信息
SELECT *
FROM course
WHERE Cname='数据库原理及应用'
#[19]查询每门(被选修)课程的课程号以及选修该课程的学生信息，并按课程号升序进行排列
SELECT score.Cno,student.*
FROM score JOIN student
ON score.Sno=student.Sno
ORDER BY Cno ASC


```


