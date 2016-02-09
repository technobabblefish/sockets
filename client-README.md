# sockets

//Receives socket data from server until EOF, then catches error
// needed for multiline data like netstat

package clientserver;

/**
 *
 * @author n00
 */
import java.io.*;
import java.lang.ClassNotFoundException;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;

public class Clientserver {

    public static void main(String[] args) {
        System.out.println("Starting client main: . . . ");
        try {
            //
            // Create a connection to the server socket on the server application
            //
            InetAddress host = InetAddress.getLocalHost();
            Socket socket = new Socket(host.getHostName(), 7777);

            //
            // Send a message to the client application
            //
            ObjectOutputStream oos = new ObjectOutputStream(socket.getOutputStream());
            oos.writeObject(menuItem);

            //
            // Read and display the response message sent by server application
            //
            ObjectInputStream ois = new ObjectInputStream(socket.getInputStream());
            String message;
            try {
                   while( (message = (String) ois.readObject()) != null){
            System.out.println("Received from server: " + message);
                   }
            } catch (EOFException e){
                /// end of stream
            }

            ois.close();
            oos.close();
        } catch (UnknownHostException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
