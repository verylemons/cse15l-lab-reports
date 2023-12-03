**LAB REPORT 5**
**Kwae Htoo, A17327141**

- The java files and bash scripts that I will be using are the bash script that grades a student's ListExamples.java. Here is the link to the repository: **https://github.com/verylemons/Lab-Report-5_Design/tree/main**
- The bug/issue is located in the bash script "grade.sh" file. Specifically, there's an issue when compiling and running the script.

**1. The original post from a student with a screenshot showing a symptom and a description of a guess at the bug/some sense of what the failure-inducing input is.**

**Patrick Star** *student*

"There seems to be an issue when I run the bash script. It says that the compiling is unsuccessful and that the junit file doesn't exist. I think that's where the bug is. I don't know what is wrong with the line of code that is used to compile the code."

<img width="770" alt="Screen Shot 2023-12-03 at 1 47 36 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/bd8e3e2a-27c7-40e1-b49b-7ae905bbb0c8">

<img width="929" alt="Screen Shot 2023-12-03 at 1 39 27 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/18c9f3fa-f906-48fc-b3c8-d239e2518c44">

**2. A response from a TA asking a leading question or suggesting a command to try**

**SpongeBob SquarePants** *staff*

"If it's saying that the junit file cannot be found, then there must be something wrong with the path, right? Take a look at the line of code before the javac compile line. What are you doing there? Then, take a look at the path that you are using to compile."

**3. Another screenshot/terminal output showing what information the student got from trying that, and a clear description of what the bug is.**

**Patrick Star** *student*

<img width="785" alt="Screen Shot 2023-12-03 at 1 59 29 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/ce30880b-0336-4646-965d-206e31b3f38d">

<img width="909" alt="Screen Shot 2023-12-03 at 1 59 42 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/1937179b-1979-47e6-ba99-edc3155914dc">

"I see where the issue was. It was with the path. Since there was a command the changed the directory into the grading-area directory, the lib file was is not located in that directory, therefore, I needed to go out one directory in the path so the lib folder containing the junit files could be found."

**4. At the end, all the information needed about the setup including:**

- **The file & directory structure needed**
  - list-examples-grader
    - lib
      - hamcrest-core-1.3.jar
      - junit-4.13.2.jar
    - grade.sh
    - GradeServer.java
    - Server.java
    - TestListExamples.java
  
- **The contents of each file before fixing the bug**
  - Inside **grade.sh**

``
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'


if test -f "student-submission/ListExamples.java"; then
echo ""
echo "Correct File Submitted"
echo ""
else
echo "Incorrect File Submitted"
exit
fi

cp student-submission/ListExamples.java grading-area
cp TestListExamples.java grading-area

cd grading-area/
javac -cp .:/lib/hamcrest-core-1.3.jar:/lib/junit-4.13.2.jar *.java

if test $? -eq 0; then
echo "Successful Compile"
echo ""
else
echo "Unsuccessful Compile"
exit
fi

java -cp .:/lib/hamcrest-core-1.3.jar:/lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > results.txt

if echo "OK (1 test)" | grep "OK (1 test)" results.txt; then
echo "You passed!"
else
echo "You Failed!"
fi
``
