**LAB REPORT 4**
**Kwae Htoo, A17327141**

**4. Log into ieng6**

<img width="690" alt="Screen Shot 2023-11-19 at 11 54 53 AM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/7bfc2b4a-3d87-4c0f-8e93-b2dc992f74e8">

Keys/commands pressed: ssh cs15lfa23an@ieng6.ucsd.edu \<enter\>
- I logged into my ieng6 account by using the command "ssh cs15lfa23an@ieng6.ucsd.edu" then pressing \<enter\>.

**5. Clone your fork of the repository from your Github account (using the SSH URL)**

<img width="735" alt="Screen Shot 2023-11-19 at 12 01 38 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/0d2a272e-f928-425a-b664-4d423423fe8b">

Keys/commands pressed: git clone git@github.com:verylemons/lab7.git \<enter\>
- I cloned my fork of the lab7 directory using the ssh url by using the command, git clone git@github.com:verylemons/lab7.git, then pressing enter.

**6. Run the tests, demonstrating that they fail**

<img width="620" alt="Screen Shot 2023-11-19 at 12 56 56 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/e6196afd-9ccf-4f7a-aad7-33b1ab307f93">

Keys/commands pressed: javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java /<enter/> bash test.sh /<enter/>
- First, I compiled the files by using the command, javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java, then pressing enter. After, to run the tests, I used the bash command, bash test.sh, then pressed enter. This showed that there was one failure.

**7. Edit the code file to fix the failing test**

<img width="349" alt="Screen Shot 2023-11-19 at 1 03 21 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/ba82e3bf-5347-43fe-8b0a-de0f638ce588">

Keys/commands pressed: "GG" \<up\>\<up\>\<up\>\<up\>\<up\>\<up\>\<right\>\<right\>\<right\>\<right\>\<right\>\<right\>\<right\>\<right\>\<right\>\<right\>\<right\> "a" \<backspace\> "2" \<escape\> ":wq"
- I used the "vim ListExamples.java" command to enter into the vim editor to edit the file that needed fixing. Then I typed "GG" to go to the last line in the file because the part that I needed to fix was closer to the end. After, I pressed the \<up\> key 6 times to go the line that needed fixing. I needed to change index1 to index2, therefore, I pressed the \<right\> key 11 times to go on top of the "1" in "index2". After I pressed "a" to enter insert mode and edit the place where I was at. I pressed the \<backspace\> key to delete the "1" and change it into a 2. Then I pressed the \<escape\> key to return to normal mode. Finally, I typed ":wq" to save my changes and exit vim.

