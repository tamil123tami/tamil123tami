import mysql.connector as sql
from tabulate import tabulate
con=sql.connect(host="localhost",user='root',password='',database="bookstor
e")
if con.is_connected():
 print('successfully connected')
def insert():
 name=input("Enter Name:")
 author = input("Enter of the author: ")
 rate = int(input("Enter the amount: "))
 BOOKNO= int(input("enter the bookno:"))
 res=con.cursor()
 sql="insert into books(name,author,rate,BOOKNO) values(%s,%s,%s,%s)"
 res.execute(sql, (name,author,rate,BOOKNO))
 con.commit()
 print("\n")
 print("Record Insert Successfully")
def select():
 res = con.cursor()
 sql= "SELECT * from books"
 res.execute(sql)
 result = res.fetchall()
 print("\n")
 print(tabulate(result, headers=["NO","ID", "NAME", "AUTHOR", "RATE"]))
def update():
 print("1.NAME")
 print("2.AUTHOR")
 print("3.RATE")
 choice=int(input("enter which field you want to change?"))
 if choice==1:
 BOOKNO=int(input("enter the BOOKNO:"))
 name=input("enter the name:")
 cur=con.cursor()
 sql="UPDATE books set name=%s where BOOKNO=%s"
 cur.execute(sql,(name,BOOKNO))
 con.commit()
 select()
 print("\n")
 print("Update succesfully")
 elif choice==2:
 BOOKNO = int(input("enter the BOOKNO:"))
 author = input("enter the author's name:")
 cur = con.cursor()
 sql = "UPDATE books set author=%s where BOOKNO=%s"
 cur.execute(sql, (author, BOOKNO))
 con.commit()
 select()
 print("\n")
 print("Update succesfully")
 elif choice == 3:
 BOOKNO = int(input("enter the BOOKNO:"))
 rate = int(input("enter the amount:"))
 cur = con.cursor()
 sql = "UPDATE books set rate=%s where BOOKNO=%s"
 cur.execute(sql, (rate, BOOKNO))
 con.commit()
 else:
 print("invalid")
def delete():
 bookID = input("enter the bookid:")
 res = con.cursor()
 sql = "DELETE FROM books WHERE bookID=%s"
 res.execute(sql,(bookID,))
 con.commit()
 print("\n")
 print("Record Insert Successfully")
def search_cust():
 a=int(input("ENTER 1.FOR SEARCHING NAME (OR)2.FOR SEARCHING BOOKNO:"))
 if a==1:
 NAME = input("enter the name=")
 res=con.cursor()
 sql = "SELECT * from customer WHERE NAME=%s"
 res.execute(sql,(NAME,))
 result = res.fetchall()
 print("\n")
 print(tabulate(result, headers=["S_NO", "BOOKNO", 
"NAME","book_name", "AUTHOR", "RATE","DATE","PHONE_NO"]))
 elif a==2:
 BOOKNO = int(input("enter the BOOKNO="))
 res = con.cursor()
 sql = "SELECT * from customer WHERE BOOKNO=%s"
 res.execute(sql, (BOOKNO,))
 result = res.fetchall()
 print("\n")
 print(tabulate(result, headers=["S_NO", "BOOKNO", "NAME", 
"book_name", "AUTHOR", "RATE", "DATE", "PHONE_NO"]))
 else:
 print("INVALID")
def insert_cust():
 S_NO= int(input("Enter the SERIAL NO:"))
 BOOKNO = int(input("Enter the bookno:"))
 NAME= input("Enter Customer Name:")
 book_name= input("Enter of the bookname: ")
 AUTHOR= input("Enter the author:")
 AMOUNT= int(input("enter the amount:"))
 PHONE_NO=int(input("Enter the phone:"))
 res = con.cursor()
 sql = "insert into customer(S_NO,BOOKNO, NAME,book_name, AUTHOR, 
AMOUNT,PHONE_NO,DATE) values(%s,%s,%s,%s,%s,%s,%s,NOW())"
 res.execute(sql, (S_NO,BOOKNO, NAME,book_name, AUTHOR, 
AMOUNT,PHONE_NO))
 con.commit()
 print("\n")
 print("Record Insert Successfully")
def cust_delete():
 S_NO= input("enter the serial no:")
 res = con.cursor()
 sql = "DELETE FROM customer WHERE S_NO=%s"
 res.execute(sql,( S_NO,))
 con.commit()
 print("\n")
 print("Record Insert Successfully")
def display_cust():
 res = con.cursor()
 sql= "SELECT * from customer"
 res.execute(sql)
 result = res.fetchall()
 print("\n")
 print(tabulate(result, headers=["S_NO", "BOOKNO", "NAME","book_name", 
"AUTHOR", "RATE","DATE","PHONE_NO"]))
while True:
 print("\n")
 print("\t BOOK AVAILABILITY RECORD")
 print("1.Insert Record")
 print("2.Display Record")
 print("3.Update Record")
 print("4.Delete Record")
 print("\t CUSTOMER INFORMATION")
 print("5.Search For A Particular Customer")
 print("6.Insert Customer")
 print("7.Delete Customer record")
 print("8.Display All Customer Record")
 print("9.Exit")
 print("\n")
 choice = int(input("Enter Your Choice :"))
 if choice == 1:
 insert()
 elif choice == 2:
 select()
 elif choice == 3:
 update()
 elif choice == 4:
 delete()
 elif choice == 5:
 search_cust()
 elif choice == 6:
 insert_cust()
 elif choice == 7:
 cust_delete()
 elif choice == 8:
 display_cust()
 elif choice == 9:
 print("OVER AND OUT")
 quit()
else:
 print("InvalidOption...!!!")>
