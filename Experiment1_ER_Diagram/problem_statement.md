# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="1154" height="804" alt="image" src="https://github.com/user-attachments/assets/c8984a33-eed8-4db2-9c32-47c352ea9a55" />


### Entities and Attributes

1. Member (MemberID PK, Name, MembershipType, StartDate) 
2. Program (ProgramID PK, Name, Type) 
3. Trainer (TrainerID PK, Name, Specialization) 
4. Session (SessionID PK, Date, Time, Duration) 
5. Payment (PaymentID PK, Amount, Date, Type [Membership/Session]) 
6. Attendance (AttendanceID PK, Status, Date) 

### Relationships and Constraints

• Member – Program: M:N (A member can join multiple programs; a program can have 
multiple members). 
• Program – Trainer: M:N (A program may have multiple trainers; trainers can manage 
multiple programs). 
• Member – Trainer – Session: M:N via Session (Members book personal training sessions 
with trainers). 
• Session – Attendance: 1:N (One session has multiple attendance records). 
• Member – Payment: 1:N (One member makes multiple payments).

### Assumptions

• Membership fees and session fees are both stored in Payment. 
• Personal training sessions are treated separately from group programs. 
• Attendance is recorded per session per member. 

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="803" height="431" alt="image" src="https://github.com/user-attachments/assets/43b0ede9-44f7-4095-8388-f1bbbc31e97f" />


### Entities and Attributes

1. Member (MemberID PK, Name, Email, Phone) 
2. Book (BookID PK, Title, Author, Category) 
3. Loan (LoanID PK, LoanDate, ReturnDate, Fine) 
4. Event (EventID PK, Name, Date, Description) 
5. Speaker (SpeakerID PK, Name, Bio, Expertise) 
6. Room (RoomID PK, RoomName, Capacity) 

### Relationships and Constraints

• Member – Book – Loan: M:N via Loan (A member can borrow multiple books; each book 
may be borrowed by multiple members). 
• Member – Event: M:N (A member may register for many events; each event has many 
registered members). 
• Event – Speaker: M:N (An event may have multiple speakers; speakers can appear at 
multiple events). 
• Event – Room: 1:1 per event (An event is assigned one room; a room can host many events 
over time but only one at a given date/time). 

### Assumptions

• Overdue fines are tracked as an attribute in Loan. 
• Events always happen in a single room. 
• Books are uniquely identified by BookID, even if multiple copies exist (copies can be an 
extension if needed). 

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="580" height="671" alt="image" src="https://github.com/user-attachments/assets/9fd3f48b-76f3-45cc-93e8-52cc3ab426fc" />


### Entities and Attributes

1. Customer (CustomerID PK, Name, Phone, Email) 
2. Reservation (ReservationID PK, Date, Time, Guests) 
3. Order (OrderID PK, OrderTime, Status) 
4. Dish (DishID PK, Name, Price, Category) 
5. Bill (BillID PK, Amount, Date, ServiceCharge) 
6. Waiter (WaiterID PK, Name, Shift)

### Relationships and Constraints

• Customer – Reservation: 1:N (A customer can have multiple reservations). 
• Reservation – Order: 1:N (Each reservation can place multiple orders). 
• Order – Dish: M:N (An order contains multiple dishes; a dish may appear in multiple orders). 
• Reservation – Bill: 1:1 (One reservation generates one bill). 
• Reservation – Waiter: M:N (A reservation may be served by multiple waiters; waiters handle 
multiple reservations).

### Assumptions

• Every reservation must have a customer linked to it (even walk-ins). 
• Each bill corresponds to exactly one reservation. 
• Dishes belong to categories such as starter, main, dessert. 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
