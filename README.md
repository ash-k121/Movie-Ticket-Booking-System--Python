# Movie-Ticket-Booking-System--Python
# An interface between a user and a movie theatre which helps you to book tickets online for your preferred city .Users get discounts based on their interaction with the platform.

import mysql.connector
db=mysql.connector.connect(host="localhost",user="root",password="tiger")
cursor=db.cursor()
database=cursor.execute('Create database MovieBooth;')
cursor.execute('Use Moviebooth;')
# Creation of Main tables
cursor.execute('''Create table Book(Ticketcode int(5) primary key,Name varchar(20),Age int(3),City varchar(15),
Center varchar(20),Movie varchar(20),ModeOfPayment varchar(10),Discount int,Points int);''')
# Creation of Seat Tables
cursor.execute("Create table Seat(A varchar(5),B varchar(5),C varchar(5),D varchar(5),E varchar(5),F varchar(5),G varchar(5));")
cursor.execute("insert into seat values('B',1,2,3,4,5,6);")
cursor.execute("insert into seat values('C',7,8,9,10,11,12);")
cursor.execute("insert into seat values('D',13,14,15,16,17,18);")
cursor.execute("insert into seat values('E',19,20,21,22,23,24);")
cursor.execute("insert into seat values('F',25,26,27,28,29,30);")
cursor.execute("insert into seat values('G',31,32,33,34,35,36);")
cursor.execute("insert into seat values('H',37,38,39,40,41,42)")
db.commit()

import sys
from termcolor import colored,cprint
text = colored('WELCOME TO YOUR MOVIE BOOTH', 'red', attrs=['reverse', 'blink'])
print(text)
def data():
    text = colored('Enter Name And Age', 'green', attrs=['reverse', 'blink'])
    print(text)
    name=input("Kindly Enter Your Name:")
    age=int(input("Kindly Enter Your Age:"))
    text=colored('Enter City', 'blue', attrs=['reverse', 'blink'])
    print(text)
    print("Choose The City Among The Mentioned Below:")
    print("""
      CITY 1
      CITY 2
      CITY 3
      CITY 4""")
    city=int(input("Choose your City: "))
    if city==1:
        city='City1'
    elif city==2:
        city='City2'
    elif city==3:
        city='City3'   
    elif city==4:
        city='City4'
    else:
        city='NULL'
        cprint("Invalid Option!", 'red', attrs=['bold'], file=sys.stderr)

    text = colored('Enter Movie', 'blue', attrs=['reverse', 'blink'])
    print(text)
    print("Choose The Movie To Watch")
    print("""
      1:Movie1
      2:Movie2
      3:Movie3
      4:Movie4
      5:Movie5""")
    movie = int(input("Choose your Movie: "))
    if movie==1:
        movie='Movie1'
    elif movie==2:
        movie='Movie2'
    elif movie==3:
        movie='Movie3'
    elif movie==4:
        movie='Movie4'
    elif movie==5:
        movie='Movie5'
    else:
        movie='NULL'
        cprint("Invalid Option!", 'red', attrs=['bold'], file=sys.stderr)
        
        
    from datetime import date
    today=date.today()
    print("TICKETS CAN BE BOOKED ON :")
    print(">",today.day,"/",today.month,"/",today.year,'(Enter 1)')
    print(">",today.day+1,"/",today.month,"/",today.year,'(Enter 2)')
    print(">",today.day+2,"/",today.month,"/",today.year,'(Enter 3)')
    day=int(input('Enter choice:'))
    
    print("Movie Day")
    time1 = {"1": "10.00-1.00","2": "1.10-4.10","3": "4.20-7.20"}
    time2 = {"1": "10.15-1.15","2": "1.25-4.25", "3": "4.35-7.35"}
    time3 = {"1": "10.30-1.30","2": "1.40-4.40", "3": "4.50-7.50"}
    if day==1:
        print("choose your time:")
        print(time1)
        t = input("select your time:")
        x = time1[t]
        cprint("SUCCESSFUL!,ENJOY MOVIE AT  "+x,'blue', attrs=['bold'], file=sys.stderr)
    elif day==2:
        print("choose your time:")
        print(time2)
        t = input("select your time:")
        x = time2[t]
        cprint("SUCCESSFUL!,ENJOY MOVIE AT  " +x,'blue', attrs=['bold'], file=sys.stderr)
    elif day==3:
        print("choose your time:")
        print(time3)
        t = input("select your time:")
        x = time3[t]
        cprint("SUCCESSFUL!,ENJOY MOVIE AT  "+x,'blue', attrs=['bold'], file=sys.stderr)
    else:
        cprint("Invalid Option!", 'red', attrs=['bold'], file=sys.stderr)
        
        
    text = colored('Enter Center', 'green', attrs=['reverse', 'blink'])
    print(text)
    print("Which theater do you wish to see movie? ")
    print("1.Inox")
    print("2.Icon")
    print("3.PVR")
    print("4.Wave")
    print("5.Carnival")
    center = int(input("Choose your Option: "))
    if center==1:
        center='Inox'
    elif center==2:
        center='Icon'
    elif center==3:
        center='PVR'
    elif center==4:
        center='Wave'
    elif center==5:
        center='Carnival'
    else:
        cprint("Invalid Option!", 'red', attrs=['bold'], file=sys.stderr)
        
      
    
    text = colored('Book Your Seat', 'cyan', attrs=['reverse', 'blink'])
    print(text)
    # SEAT TABLE IN DATABASE-MOVIEBOOTH TABLENAME-SEAT  
    from tabulate import tabulate
    cursor.execute("select * from SEAT;")
    table=[]
    l=('A','B','C','D','E','F','G')
    table.append(l)
    for i in cursor:
        table.append(i)    
    print(tabulate(table, headers='firstrow', tablefmt='fancy_grid'))
    n1=int(input('Enter Seat Number to Book')) 
    columnname=input('Enter Column Name')
    columnname=columnname.upper()
    n2='X'
    if n1>=1 and n1<=6:
        cursor.execute(f"update SEAT set {columnname}='{n2}' where A='B';")
        db.commit()
    elif n1>=7 and n1<=12:
        cursor.execute(f"update SEAT set {columnname}='{n2}' where A='C';")
        db.commit()
    elif n1>=13 and n1<=18:
        cursor.execute(f"update SEAT set {columnname}='{n2}'where A='D';")
        db.commit()
    elif n1>=19 and n1<=24:
        cursor.execute(f"update SEAT set {columnname}='{n2}' where A='E';")
        db.commit()
    elif n1>=25 and n1<=30:
        cursor.execute(f"update SEAT set {columnname}='{n2}' where A='F';")
        db.commit()
    elif n1>=31 and n1<=36:
        cursor.execute(f"update SEAT set {columnname}='{n2}' where A='G';")
        db.commit()
    elif n1>=37 and n1<=42:
        cursor.execute(f"update SEAT set {columnname}='{n2}' where A='H';")
        db.commit()
    cursor.execute("select * from SEAT")
    table=[]
    l=('A','B','C','D','E','F','G')
    table.append(l)
    for i in cursor:
        table.append(i)    
    print(tabulate(table, headers='firstrow', tablefmt='fancy_grid'))  
    text = colored('Mode of Payment', 'yellow', attrs=['reverse', 'blink'])
    print(text)
    print('''How do you wish to pay?
             1.Cash
             2.Card(Avail Discount/Points)''')
    points=0
    mod=(input('''Enter 1 for Cash \n Enter 2 for Card'''))
    if mod=='2':
        price=0
        discount=0
        mod='Card'
        print('''Select Card \n   1.Credit Card(Enter 1) \n   2.Debit Card(Enter 2)''')
        card=input('Enter Card type')
        print('''  1. SBI(Enter 1) \n  2. KOTAK MAHINDRA BANK(Enter 2) \n  3. ICICI BANK(Enter 3) \n  4. HDFC BANK(Enter 4)''')
        bank=input('Enter Bank : ')
        if numberoftickets>3:
            cprint("CONGRATULATIONS YOU ARE GIVEN A DISCOUNT OF 25%", 'yellow', attrs=['bold'], file=sys.stderr)
            discount=75 
            price=225
            points=100
        else:
            price=300
            points=100
            pass
        if bank=='1' or bank=='2'or bank=='3'or bank=='4':
            cprint("CONGRATULATIONS YOU AVAILED 100 POINTS IN YOUR MOVIEBOOTH ACCOUNT", 'yellow', attrs=['bold'], file=sys.stderr)
    elif mod=='1':
        price=0
        discount=0
        mod='cash'
        if numberoftickets>3: 
            cprint("CONGRATULATIONS YOU ARE GIVEN A DISCOUNT OF 25%", 'yellow', attrs=['bold'], file=sys.stderr)
            discount=75
            price=225
        else:
            price=300
            mod='cash'
            print("YOUR TOTAL AMOUNT IS",price)
    else:
        cprint("Invalid Option!", 'red', attrs=['bold'], file=sys.stderr)
    cprint("TICKET BOOKED SUCCESSFULLY  ",'blue', attrs=['bold'], file=sys.stderr)
    import random
    global b
    b=[]
    code=" "
    for i in range(0,5):
        a=random.randint(0,9)
        code+=str(a)  
    if code not in b:
        b.append(code)
    else:
        pass
    print('Your Ticket Code: ',code)
   
    table=[]
    head = ["TICKET CODE ","NAME","NAME OF THE MOVIE","THEATER","PAID AMOUNT","DISCOUNT","POINTS"]
    table.append(head)
    l=(code,name,movie,center,price,discount,points)
    table.append(l)  
    print(tabulate(table, headers='firstrow', tablefmt='fancy_grid'))
    cursor.execute('Use MovieBooth;')
    rec=(code,name,age,city,center,movie,mod,price,discount,points)
    query="INSERT INTO book VALUES(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"
    cursor.execute(query,rec)
    db.commit()

numberoftickets=int(input('Enter number of tickets'))
for i in range(numberoftickets):
    data()    
def Display():
    text = colored('Display', 'yellow', attrs=['reverse', 'blink'])
    print(text)
    from tabulate import tabulate
    cursor.execute("select * from book")
    table=[]
    columnname=('TicketCode','Name','Age','City','Center','Movie','ModeofPayment','Price','Discount','Points')
    table.append(columnname)
    for i in cursor:
        table.append(i)  
    print(tabulate(table, headers='firstrow', tablefmt='fancy_grid'))


def Modify():
    tnumber=input("Enter Ticket Code")
    if len(tnumber)==5:
        print("Your Ticket code is Valid")
    else:
        print("Kindly Check,Your Ticket Code is Invalid")
    text = colored('Modify', 'yellow', attrs=['reverse', 'blink'])
    print(text)
    print("""Choose Among the Given Options
    1: modify age
    2: modify name
    3: modify movie""")
    tnumber=int(tnumber)
    option=int(input("Enter The Option"))
    if option==1:
        data=int(input("Enter the Modified Age"))
        query="update book set age=%s where ticketcode=%s"
        new=(data,tnumber)
        cursor.execute(query,new)
        db.commit()
    elif option==2:
        data=input("Enter the Modified Name")
        query="update book set name=%s where ticketcode=%s"
        new=(data,tnumber)
        cursor.execute(query,new)
        db.commit()
    else:
        print("Select Movie Among The Mentioned Options")
        print("""
        1:Movie1
        2:Movie2
        3:Movie3
        4:Movie4
        5:Movie5""")
        Movie = int(input("Choose The Movie To Watch: "))
        if Movie==1:
            Movie='Movie1'
        elif Movie==2:
            Movie='Movie2'
        elif Movie==3:
            Movie='Movie3'
        elif Movie==4:
            Movie='Movie4'
        elif Movie==5:
            Movie='Movie5'
        else:
            cprint("INVALID OPTION!", 'red', attrs=['bold'], file=sys.stderr)
        query="update book set movie=%s where ticketcode=%s"
        new=(Movie,tnumber)
        cursor.execute(query,new)
        db.commit()
        cprint("SUCCESSFULLY MODIFIED!", 'blue', attrs=['bold'], file=sys.stderr)
def Cancel():
    text = colored('Cancel', 'blue', attrs=['reverse', 'blink'])
    print(text)
    print('Are you Sure? Yes/No')
    ans=input('Enter yes/no:')
    ans=ans.lower()
    if ans=='yes':
        tnumber=(input("Enter Ticket Code"))
        query="DELETE FROM book WHERE ticketcode=%s"
        new=(tnumber,)
        cursor.execute(query,new)
        db.commit()
    elif ans=='no':
        print('OK')
def Rating():
    print("It will be highly appreciable if you give us rating")
    print("""Rate us:
    1: EXCELLENT *
    2: VERY GOOD **
    3: GOOD      *
    4: AVERAGE   **""")
    choice=input("Kindly Enter Your Choice")
    cprint("THANK YOU FOR YOUR RATING !! ",'magenta', attrs=['reverse', 'blink'])

def functions():
    print("""Select Your Choice Among Mentioned Below  
    1.Display Records
    2.Cancellation of Ticket
    3.Modify
    4.Rating
    5.Quit""")
    choice=int(input("Kindly Enter Your Choice"))
    if choice==1:
        Display()
    elif choice==2:
        Cancel()
    elif choice==3:
        Modify()
    elif choice==4:
        Rating()
    elif choice==5:
        print('Quiting')
    else:
        cprint("Invalid Option!", 'red', attrs=['bold'], file=sys.stderr)
functions()
while True:
    ch=input('Do You Wish To Continue?  y/n')
    if ch in'yY':
        functions()
    elif ch in 'nN':
        break  
    else:
        cprint("Invalid Option!", 'red', attrs=['bold'], file=sys.stderr)

