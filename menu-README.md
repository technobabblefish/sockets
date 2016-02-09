# sockets
menu:
import java.io.*;
import java.util.*;

public class exec2 {

public static void main(String[] args) throws IOException {

            // A Runtime object has methods for dealing with the OS
Runtime r = Runtime.getRuntime();
Process p;     // Process tracks one external native process
BufferedReader is;  // reader for output of process
String line;
Scanner menuSel = new Scanner(System.in);

// menu selection
char c = 0;

Date test = new Date();
long startTime = 1;
long endTime = 10;


mLoop: while (c != 7) {

System.out.println(" === MENU === \n");
System.out.println("1. Host current Date and Time ");
System.out.println("2. Host uptime ");
System.out.println("3. Host memory use ");
System.out.println("4. Host Netstat ");
System.out.println("5. Host current users ");
System.out.println("6. Host running processes ");
System.out.println("7. Quit \n");
System.out.print("\n>>>>>  ");

c = menuSel.next().charAt(0);


// System.out.println("Selected character:  " + c + "...");

switch (c) {
        case '1':
        System.out.print("\nDate: ");
        startTime = System.nanoTime();
        p = r.exec("date");
        endTime = System.nanoTime();
        break;

        case '2':
        System.out.print("\nuptime: ");
        p = r.exec("uptime");
        break;
        case '3':
        System.out.print("\nfree memory: \n");
        p = r.exec("free");
        break;
        case '4':
        p = r.exec("netstat");
        break;
        case '5':
        p = r.exec("who");
        break;
        case '6':
        p = r.exec("ps");
        break;
        case '7':
      //  p = r.exec("ls");
        break mLoop;
       //  break;

  default:
       System.out.println("Invalid selection.");
       p=r.exec("echo Invalid");
       break;
} // end switch menu



  //  System.out.println("In Main after exec");

    // getInputStream gives an Input stream connected to
    // the process p's standard output. Just use it to make
    // a BufferedReader to readLine() what the program writes out.
    is = new BufferedReader(new InputStreamReader(p.getInputStream()));

//    startTime = getTime();

    while ((line = is.readLine()) != null)
      System.out.println(line);

    System.out.flush();
    try {
      p.waitFor();  // wait for process to complete
      long loopTime = endTime - startTime;
      System.out.println("Time in loop:  " + loopTime + "(Starttime " + startTim                                                                                                                                e + " minus endtime " + endTime + ".\n" );
    } catch (InterruptedException e) {
      System.err.println(e);  // "Can'tHappen"
      return;
    }
  } //end while
 //   endTime = getime();

//    long diffTime = endTime - startTime;
 //   System.out.println("Time taken in mills:  " + diffTime);

        // end the program -- close sockets?
    System.out.println("\n-----\nDone.");
    return;

}

}
