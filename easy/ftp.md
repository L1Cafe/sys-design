# Describe FTP

File Transfer Protocol (FTP) is a standard network protocol used for transferring files between computers over a network. Developed in the early 1970s, FTP was one of the first protocols used on the internet and remains widely used today for file sharing and transfers.

FTP operates based on a client-server model. The client, which is the computer initiating the connection, connects to the server, which is the computer hosting the files. The client then requests a file transfer by specifying the files and directories to upload or download. The server will respond with a list of available files and directories, allowing the client to select which files to transfer.

FTP uses two separate communication channels between the client and server:

- A control channel for commands, such as requesting file transfers, deleting files, or closing the connection.
- A data channel for the actual file data being transferred.

The FTP protocol supports different transfer modes depending on the type of file. ASCII mode is used for transferring text files, while binary mode is used for all other file types. FTP also includes support for both passive and active transfer modes, which determine how the data channel is established between the client and server.

