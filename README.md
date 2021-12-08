# university-database
Implementation of a university database for CS 340 Introduction to Databases

## Entity-Relationship Diagram
![image](https://user-images.githubusercontent.com/71689421/145125503-29a3ccce-e3ca-4a0b-80d2-9febb2fbbc04.png)

## Schema
![image](https://user-images.githubusercontent.com/71689421/145124235-8312dd54-1c19-4762-9d9e-84214b74b500.png)

## Screen Captures
#### 1. READ/BROWSE/DISPLAY Students and DELETE Student page
![image](https://user-images.githubusercontent.com/71689421/145124442-6d6aee0c-a2bf-49f2-8ab1-3f524917e472.png)

#### 2. CREATE/INSERT/ADD NEW Student page
![image](https://user-images.githubusercontent.com/71689421/145124476-3146ab90-1f55-4c96-91f2-856d953a8d97.png)

#### 3. READ/BROWSE/DISPLAY Courses and DELETE Course page
![image](https://user-images.githubusercontent.com/71689421/145124509-48ea3e7a-f13d-4ce9-8f00-c83668581646.png)

#### 4. CREATE/INSERT/ADD NEW Course page
![image](https://user-images.githubusercontent.com/71689421/145124556-7b6d3d13-296b-41d1-b297-a6c013979e30.png)

#### 5. READ/BROWSE/DISPLAY Sections, SEARCH/FILTER Sections and DELETE Section page
![image](https://user-images.githubusercontent.com/71689421/145124591-cefaf8f0-0f96-4a85-8d05-bd0bd80bbb10.png)

#### 6. CREATE/INSERT/ADD NEW Section page
![image](https://user-images.githubusercontent.com/71689421/145124648-d0f709ea-1791-4a74-95b8-dab873081b76.png)

#### 7. READ/BROWSE/DISPLAY Instructors and DELETE Instructor page
![image](https://user-images.githubusercontent.com/71689421/145124679-76d8220f-b20b-47be-9cae-a10914ae1adc.png)

#### 8. CREATE/INSERT/ADD NEW Instructor page
![image](https://user-images.githubusercontent.com/71689421/145125408-691e398f-ad36-457e-a648-3bd82e6c0079.png)

#### 9. EDIT/UPDATE an INSTRUCTOR page
![image](https://user-images.githubusercontent.com/71689421/145125381-e37ff415-a973-44dd-9721-2da2cfa0dbfa.png)

#### 10. READ/BROWSE/DISPLAY Campuses and DELETE Campus page
![image](https://user-images.githubusercontent.com/71689421/145125357-a302a20e-652b-48d9-835e-fa092209d36e.png)

#### 11. CREATE/INSERT/ADD NEW Campus page
![image](https://user-images.githubusercontent.com/71689421/145125321-e03e83ff-53f8-4f48-b813-938edc723ff6.png)

#### 12. EDIT/UPDATE a Campus page
![image](https://user-images.githubusercontent.com/71689421/145125017-6e444f22-1d5d-400e-b7e2-88c7a3e61039.png)

#### 13. READ/BROWSE/DISPLAY Students_Sections, DELETE Student_Section page, and CREATE/INSERT/ADD NEW Student_Section page
![image](https://user-images.githubusercontent.com/71689421/145124982-f6dca622-3527-425f-aaa6-153dee09cac7.png)

#### 14. READ/BROWSE/DISPLAY Courses_Campuses, DELETE Course_Campuse page, and CREATE/INSERT/ADD NEW Course_Campuse page
![image](https://user-images.githubusercontent.com/71689421/145124956-cafcaf39-1ed8-427c-b51a-988f311ed371.png)


## Database Outline, in Words
#### [ Entities ]
Courses: records the courses taught at AH University \
● course_id: int, auto_increment, unique, not NULL, PK (Primary Key) \
● course_name: varchar(255), unique

Students: records the students that are enrolled at AH University \
● student_id: int, auto_increment, unique, not NULL, PK (Primary Key) \
● student_first_name: varchar(255), not NULL \
● student_last_name: varchar(255), not NULL \
● campus_id: int, not NULL, FK (Foreign Key) \

Instructors: records the instructors that lecture at AH University \
● instructor_id: int, auto_increment, unique, not NULL, PK (Primary Key) \
● instructor_first_name: varchar(255), not NULL \
● instructor_last_name: varchar(255), not NULL \
● campus_id: int, FK (Foreign Key) \

Campuses: records the campuses offered at AH University \
● campus_id: int, auto_increment, unique, not NULL, PK (Primary Key) \
● campus_name: varchar(255), unique, not NULL \
● campus_city: text \
● campus_country: text \
● campus_online: boolean \

Sections: records the sections of courses with its campus and instructor \
● section_id: int, auto_increment, unique, not NULL, PK (Primary Key) \
● course_id: int, not NULL, FK (Foreign Key) \
● instructor_id: int, not NULL, FK (Foreign Key) \
● campus_id: int, not NULL, FK (Foreign Key) \

#### [ Relationships ]
The Entities are related as follows:
1. A student can register for zero or more sections.
2. A section can have zero or more students enrolled in it.
3. A student can enroll in exactly one campus.
4. A campus can have zero or more students enrolled.
5. A course can be available at one or more campuses.
6. A campus can have one or more courses.
7. A course can have one or more sections.
8. A section can have exactly one course.
9. An instructor can teach at one campus at most.
10. A campus can have one or more instructors.
11. An instructor can teach zero or more sections.
12. A section can be taught by exactly one instructor.
13. A section can be available at exactly one campus.
14. A campus can have one or more sections.

#### [ Data Relationships ] 1 to M / M to M 
1. 1 to M: Campuses and Students. A student must be enrolled in exactly one campus, but
a campus can have many students enrolled. This is implemented with campus_id as a
FK (Foreign Key) inside of Students.
2. 1 to M: Campuses and Instructors. An instructor can teach at one campus at most, but a
campus can have many instructors. This is implemented with campus_id as a FK
(Foreign Key) inside of Instructors.
3. 1 to M: Courses and Sections. A course can have many sections, but a section can have
exactly one course. This is implemented with course_id as a FK (Foreign Key) inside of
Sections.
4. 1 to M: Instructors and Sections. An instructor can teach many sections, but a section
can have exactly one instructor. This is implemented with instructor_id as a FK (Foreign
Key) inside of Sections.
5. 1 to M: Campuses and Sections. A section can only be available at exactly one campus,
but a campus can have many sections. This is implemented with campus_id as a FK
(Foreign Key) inside of Sections.
6. M to M: Students and Sections. A student can register for many sections, and a section
can include many students. This is implemented by a separate relationship or
intersection table that contains a listing of which sections students are registered in and
which students are enrolled in each section. For example:
section_id (FK) student_id (FK)
7. M to M: Courses and Campuses. A course can be available at many campuses, and a
campus can have many courses. This is implemented by a separate relationship or
intersection table that contains a list of which courses are offered at each campus and
which campuses a course is taught at. For example:
course_id (FK) campus_id (FK)
