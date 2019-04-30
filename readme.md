# Multi-threaded Socket Programming - Chat Application with Java

This is a simple chat applciation. Please check Workshop - 8 SAB.pdf file to see the requirments of this workshop.

- key packages: java.net.\* package and JavaFX
- Multi-threaded socket programming: it accepts up to 10 requests from clients.

### Server-side classes

- ChatServer: This is to build an application using JavaFX
- ChatService: This is to run a thread which reads stream from client
- StartServer: This is to start a server up to 10 threads.
- User: this class includes some helper methods to manage users and sendMsg method which sends messages toward DataOutputStream to Clients

### Client-side

- Client.java: it has ConnectServer class to open communication. ConnectServer implements Runnable as the thread has to be running to keep reading data from DataInputStream

```Java
@Override
public void run() {
    try {
        socket = new Socket("localhost", 8080);

        in = new DataInputStream(socket.getInputStream());
        out = new DataOutputStream(socket.getOutputStream());

        out.writeUTF(Client.name); // send 'name' to Server
        System.out.println(Client.name + " : succesfully joined the chat room: ");

    } catch (IOException e) {
    }

    try {
        // This loop is to keep reading data from Server
        while (true) {
            String str = in.readUTF();
            Platform.runLater(() -> {
                Client.logs.setText(Client.logs.getText() + "\n" + str);
            });
        }
    } catch (IOException e) {
    }

}
```
