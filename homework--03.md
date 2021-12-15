# homework--03

```mysql
#[1] 使用SQL语句删除学生信息表(Student)中“备注”字段
ALTER TABLE student DROP COLUMN Remark
#[2] 使用SQL语句修改学生信息表(Student)中字段属性如下
#  列名	数据类型	长度	是否可空	备注
# Sname	 varchar	20	   N	     姓名
ALTER TABLE student MODIFY Sname VARCHAR(20) NOT NULL
#[3] 为Student表添加“系名”字段，存储数据如：“信息系”，“数学系”，“计算机系”等，具体数据可自行添加到Student表中
ALTER TABLE student ADD department VARCHAR(20)
#[4] 将信息系所有学生的年龄减小1岁
UPDATE student SET Birthday = Birthday + 365
WHERE student.department='信息系'
#[5] 将计算机系全体学生的成绩清零
UPDATE (score JOIN student ON score.Sno=student.Sno)
SET score.grade = 0
WHERE department='计算机系'
#[6] 删除信息系所有学生的选课记录
DELETE FROM score
WHERE score.Sno = (SELECT Sno FROM student WHERE student.department = '信息系')
#[7] 查询与“刘一平”来自同一个系的学生姓名
SELECT Sname
FROM student
WHERE department = (SELECT department FROM student where student.Sname='刘一平') AND Sname != '刘一平'
#[8] 查询其它系中’0002’ 课程比信息系所有学生分数高的学生学号和姓名
SELECT student.Sno,student.Sname
FROM score JOIN student
ON score.Sno=student.Sno
WHERE score.Cno='0002'
			AND student.department != '信息系'
			AND grade >(SELECT MAX(grade) FROM score JOIN student ON score.Sno = student.Sno WHERE department = '信息系' AND 									cno='0002')
#[9] 查询其它系中比信息系所有学生年龄大的学生姓名和性别
SELECT Sname,Sno
FROM student
WHERE ROUND(DATEDIFF(CURRENT_DATE(),Birthday)/365)>(SELECT ROUND(DATEDIFF(CURRENT_DATE(),MIN(Birthday))/365) AS 'Age'
																										FROM student
																										WHERE department = '信息系')
			AND department!='信息系'
#[10] 查询“信息系”中选课最多的学生学号
SELECT Sno
FROM(SELECT student.Sno,count(*)
		FROM student JOIN score
		ON student.Sno=score.Sno
		WHERE student.department='信息系'
		GROUP BY student.Sno
	  ORDER BY count(*) DESC) TEMPTABLE
LIMIT 0,1
#[11] 查询每门课程中低于该课程平均成绩的学生学号和姓名    ??????????????????????????????
SELECT *
FROM student JOIN score
WHERE student.Sno=score.Sno AND grade<ANY(SELECT AVG(score.Grade)
																					FROM score JOIN student
																					ON score.Sno=student.Sno
																					GROUP BY score.Cno)

Select student.sno,student.Sname
from student JOIN score x
where student.sno = x.sno and grade < (select avg(grade) from score y where y.cno=x.cno )
#[12] 统计每个系学生的平均年龄，并创建新表，同时把统计结果存入新表中
ALTER TABLE student ADD age INT

UPDATE student SET age = ROUND(DATEDIFF(CURRENT_DATE(),Birthday)/365)
WHERE age IS NULL

CREATE TABLE avgAge
SELECT department,AVG(age)
FROM student
GROUP BY department



```


