ClassRecords Smart Contract
Overview
The ClassRecords smart contract is designed to manage student records in a decentralized manner. It allows a designated teacher to add students, record grades, and retrieve the grades and names of students. The contract utilizes Solidity's error handling mechanisms (require(), assert(), and revert()) to ensure proper execution and state management.

Features
Add Student: Allows the teacher to add students to the class.
Record Grade: Allows the teacher to record grades for students.
Get Grade: Allows anyone to retrieve the grade of a student for a specific course.
Get Student Name: Allows anyone to retrieve the name of a student.
Revert and Assert Functions: Demonstrates the use of revert() and assert() statements.
Smart Contract Details

Structs
Student: Represents a student with their name, existence flag, and a mapping of course names to grades.

State Variables
teacher: Stores the address of the teacher.
students: Maps student addresses to their Student struct.
studentAddresses: Stores the list of student addresses.

Events
StudentAdded: Emitted when a student is added.
GradeRecorded: Emitted when a grade is recorded for a student.

Modifiers
onlyTeacher: Restricts function access to the teacher.
studentExists: Ensures that the student exists before executing the function.

Constructor
Sets the teacher to the address that deploys the contract.

Functions
addStudent(address studentAddress, string memory name)

Adds a new student.
Only the teacher can call this function.
Emits the StudentAdded event.
recordGrade(address studentAddress, string memory course, uint8 grade)

Records a grade for a student.
Only the teacher can call this function.
The student must exist.
The grade must be between 0 and 100.
Emits the GradeRecorded event.
getGrade(address studentAddress, string memory course) public view returns (uint8)

Retrieves the grade of a student for a specific course.
The student must exist.
getStudentName(address studentAddress) public view returns (string memory)

Retrieves the name of a student.
The student must exist.
revertIfNotTeacher() public view

Demonstrates the use of revert().
Reverts if the caller is not the teacher.
assertStudentsExist() public view

Demonstrates the use of assert().
Asserts that there are students in the class.
Usage
Deploy the Contract

Deploy the ClassRecords contract. The deployer address becomes the teacher.

Add Students

The teacher can add students using the addStudent function, specifying the student's address and name.

Record Grades

The teacher can record grades for students using the recordGrade function, specifying the student's address, course name, and grade.

Retrieve Information

Anyone can retrieve a student's grade using the getGrade function or their name using the getStudentName function.

Example
Here is an example of how to use the ClassRecords contract:

// Deploy the contract (teacher's address will be the deployer)
ClassRecords classRecords = new ClassRecords();

// Add a student (only the teacher can do this)
classRecords.addStudent(0xStudentAddress, "John Doe");

// Record a grade for the student (only the teacher can do this)
classRecords.recordGrade(0xStudentAddress, "Math", 95);

// Get the student's grade for a specific course
uint8 grade = classRecords.getGrade(0xStudentAddress, "Math");

// Get the student's name
string memory name = classRecords.getStudentName(0xStudentAddress);
Notes
The contract restricts certain functions to only be callable by the teacher using the onlyTeacher modifier.
The studentExists modifier ensures that functions interacting with students only operate on existing students.
The revertIfNotTeacher and assertStudentsExist functions demonstrate the use of revert() and assert() statements for educational purposes.
This contract is a practical example of how blockchain technology can be used to manage educational records in a transparent and secure manner.

Author:
Vageshwari Chaudhary
