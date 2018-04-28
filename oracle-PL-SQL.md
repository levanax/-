oracle:
包创建使用
```
create table tbl_company_emp
(
empno NUMBER(4) PRIMARY KEY NOT NULL,
ename VARCHAR2(10 BYTE),
job VARCHAR2(9 BYTE),
mgr NUMBER(4),
hiredate DATE,
sal NUMBER(7,2),
comm NUMBER(7,2),
deptno NUMBER(4)
);

--添加列
ALTER table tbl_company_emp add description varchar2(200) null;


--创建 包
create or replace package pkg_test is 
       v_deptno number(3):=20;
       procedure add(p_empno tbl_company_emp.empno%type);
end pkg_test;
--包体
create or replace package body pkg_test is
       procedure add(p_empno tbl_company_emp.empno%type) 
       as 
       v_empnocount NUMBER;
       begin 
         select count(*) into v_empnocount from tbl_company_emp where empno = p_empno;
         if v_empnocount = 0
           then
             insert into tbl_company_emp (empno) values  (p_empno);
             end if;
       end add;
end pkg_test;

begin
  pkg_test.add('08');
end;
```
note: 参数类型 p_empno tbl_company_emp.empno%type
