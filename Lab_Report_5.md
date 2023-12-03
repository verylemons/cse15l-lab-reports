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

"I see where the issue was. It was with the path. Since there was a command the changed the directory into the grading-area directory, the lib file was is not located in that directory, therefore, I needed to go out one directory in the path so the lib folder containing the junit files could be found."

<img width="785" alt="Screen Shot 2023-12-03 at 1 59 29 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/ce30880b-0336-4646-965d-206e31b3f38d">

<img width="909" alt="Screen Shot 2023-12-03 at 1 59 42 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/1937179b-1979-47e6-ba99-edc3155914dc">

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

```
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
```

- Inside **GradeServer.java**

```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URI;
import java.net.URISyntaxException;
import java.util.Arrays;
import java.util.stream.Stream;

class ExecHelpers {

  /**
    Takes an input stream, reads the full stream, and returns the result as a
    string.

    In Java 9 and later, new String(out.readAllBytes()) would be a better
    option, but using Java 8 for compatibility with ieng6.
  */
  static String streamToString(InputStream out) throws IOException {
    String result = "";
    while(true) {
      int c = out.read();
      if(c == -1) { break; }
      result += (char)c;
    }
    return result;
  }

  /**
    Takes a command, represented as an array of strings as it would by typed at
    the command line, runs it, and returns its combined stdout and stderr as a
    string.
  */
  static String exec(String[] cmd) throws IOException {
    Process p = new ProcessBuilder()
                    .command(Arrays.asList(cmd))
                    .redirectErrorStream(true)
                    .start();
    InputStream outputOfBash = p.getInputStream();
    return String.format("%s\n", streamToString(outputOfBash));
  }

}

class Handler implements URLHandler {
    public String handleRequest(URI url) throws IOException {
       if (url.getPath().equals("/grade")) {
           String[] parameters = url.getQuery().split("=");
           if (parameters[0].equals("repo")) {
               String[] cmd = {"bash", "grade.sh", parameters[1]};
               String result = ExecHelpers.exec(cmd);
               return result;
           }
           else {
               return "Couldn't find query parameter repo";
           }
       }
       else {
           return "Don't know how to handle that path!";
       }
    }
}

class GradeServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

class ExecExamples {
  public static void main(String[] args) throws IOException {
    String[] cmd1 = {"ls", "lib"};
    System.out.println(ExecHelpers.exec(cmd1));

    String[] cmd2 = {"pwd"};
    System.out.println(ExecHelpers.exec(cmd2));

    String[] cmd3 = {"touch", "a-new-file.txt"};
    System.out.println(ExecHelpers.exec(cmd3));
  }
}
```

- Inside **Server.java**

```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url) throws IOException;
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}
```

- Inside **TestListExamples.java**

```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }
}
```

- **The full command line (or lines) you ran to trigger the bug**

```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected
```
