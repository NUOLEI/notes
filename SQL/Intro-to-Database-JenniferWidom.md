[TOC]
# 1 Relational Algebra
In all, relational Algebra is a mathematical tool used to clarify our data query process.

## 1.1 Select Operator
pick certain rows from a relation.
For example
1. Student with GPA > 3.7
$$\sigma_{GPA > 3.7} Student$$

2. Student with GPA > 3.7 and HS < 1000
$$\sigma_{GPA > 3.7} \wedge HS <1000 Student$$ 

3. Applications to Stanford CS major
$$\sigma_{(Name='Stanford'\wedge major='cs')} Apply$$

## 1.2 Project Operator
pick certain columns
For example
1. ID and decision of all applications
$$\pi_{(sID,dec)} Apply$$

Combine them together, we can pick both rows and columns.

For example, ID and name of students with GPA > 3.7

$$\pi_{sID,name}(\sigma_{GPA>3.7}Student)$$

## 1.3 Duplicates
For example, list of application majors and decisions.

$$\pi_{major,dec} Apply$$
SQL: multisets do not drop duplicates
R.A.: sets drop duplicates

## 1.4 Cross-product
Cartesian product 笛卡尔直积
For example

$$Student \times Apply$$

![](image/Intro-to-Database-JenniferWidom/1649693788192.png)

Names and GPAs of students with HS > 1000 who applied to CS and were rejected.
![](image/Intro-to-Database-JenniferWidom/1649694158509.png)


$$\pi_{sName,GPA}(\sigma_{Student.sID=Apply.sID \wedge HS > 1000 \wedge major='CS' \wedge dec = 'Reject'}(Student \times Apply))$$

We first write this query with a big table $Student \times Apply$ to contain all the information, and then gradually expand it with select operator and porject operator.


## 1.5 Natural Join
* Enforce equility on all attributes with same equility
* Eliminate one copy of duplicate attributes

就是一个内连接和一个外连接的区别

So for the same question, withour forced equility
\bowtie
$$\pi_{sName,GPA}(\sigma_{ HS > 1000 \wedge major='CS' \wedge dec = 'Reject'}(Student \bowtie Apply))$$

Names and GPAs of students with HS > 1000 who applied to CS at college with enr > 20000 and were rejected.

$$\pi_{sName,GPA}(\sigma_{ HS > 1000 \wedge major='CS' \wedge dec = 'Reject' \wedge enr > 20000}(Student \bowtie Apply \bowtie College))$$

## 1.6 Theta Join
* Basic operation implemented in DBMS
* Term join often means theta join


$$Exp_1, \bowtie_{\theta},Exp_2 = \sigma_{\theta}(Exp_1,Exp_2)$$