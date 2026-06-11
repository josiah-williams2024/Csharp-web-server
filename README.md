# My Own Web Server

A custom HTTP web server built from scratch in C# using TCP sockets. The server processes HTTP GET requests, serves static files, returns appropriate HTTP status codes, and logs all requests and responses.

## Overview

This project demonstrates the fundamentals of web server development by implementing core HTTP functionality without using ASP.NET or other web frameworks.

The server listens for incoming TCP connections, parses HTTP requests, validates methods, locates requested resources, and returns properly formatted HTTP responses.

## Features

* Supports HTTP GET requests
* Serves static files from a configurable web root directory
* Handles common HTTP status codes
* Generates HTTP response headers
* Supports multiple file types through MIME type detection
* Request and response logging
* Error handling and server-side logging
* TCP socket-based communication

## Technologies Used

* C#
* .NET
* TCP Sockets
* NetworkStream
* File I/O
* HTTP Protocol

## Project Structure

```text
myOwnWebServer/
│
├── App.config
├── Logger.cs
├── MainProgram.cs
├── ResponseWorker.cs
├── Server.cs
├── myOwnWebServer.csproj
└── WebRoot/
    ├── index.html
    ├── sample.txt
    └── images/
```

## Architecture

### MainProgram

Application entry point responsible for:

* Reading configuration values
* Starting the server
* Initializing logging

### Server

Responsible for:

* Creating the TCP listener
* Accepting incoming client connections
* Creating ResponseWorker instances

### ResponseWorker

Handles all HTTP request processing:

* Reads client requests
* Parses HTTP request lines
* Validates HTTP methods
* Locates requested resources
* Builds HTTP responses
* Returns requested files
* Sends error responses

### Logger

Records:

* Incoming requests
* Outgoing responses
* Server errors

## Supported HTTP Methods

| Method | Supported |
| ------ | --------- |
| GET    | ✅         |
| POST   | ❌         |
| PUT    | ❌         |
| DELETE | ❌         |

Unsupported methods return:

```http
405 Method Not Allowed
```

## Supported Status Codes

| Status Code | Description           |
| ----------- | --------------------- |
| 200         | OK                    |
| 400         | Bad Request           |
| 404         | Not Found             |
| 405         | Method Not Allowed    |
| 500         | Internal Server Error |

## Supported MIME Types

| Extension | MIME Type  |
| --------- | ---------- |
| .html     | text/html  |
| .htm      | text/html  |
| .txt      | text/plain |
| .jpg      | image/jpeg |
| .jpeg     | image/jpeg |
| .gif      | image/gif  |

## Example Request

```http
GET /index.html HTTP/1.1
Host: localhost
```

## Example Response

```http
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 512
Server: myOwnWebServer
Date: Thu, 20 Nov 2025 18:00:00 GMT
Connection: close
```

## Configuration

The server is started using command-line arguments:

```bash
myOwnWebServer.exe --webRoot ./WebRoot --webIP 127.0.0.1 --webPort 8080
```

### Parameters

| Parameter | Description                          |
| --------- | ------------------------------------ |
| --webRoot | Directory containing web files       |
| --webIP   | IP address to listen on              |
| --webPort | Port number for incoming connections |

## How It Works

1. Server starts and begins listening on a TCP port.
2. Client sends an HTTP request.
3. ResponseWorker reads the request using a NetworkStream.
4. Request is parsed and validated.
5. The requested file is located.
6. MIME type is determined.
7. HTTP headers are generated.
8. File contents are sent back to the client.
9. Request and response information are logged.

## Learning Outcomes

This project demonstrates:

* TCP socket programming
* HTTP protocol fundamentals
* Request parsing
* Response generation
* File system operations
* Error handling
* Logging systems
* MIME type management
* Client-server communication

## Future Improvements

* Multi-threaded request handling
* HTTP POST support
* CSS support
* PNG image support
* Directory browsing
* HTTPS support
* Caching
* Connection keep-alive support
* Configuration file support
* Security hardening against path traversal attacks

## Example Screenshots

Add screenshots showing:

* Server startup
* Browser successfully loading a page
* Log output
* Error handling (404 page)

## Authors

* Josiah Williams
* Ricardo Gao

## References

* Microsoft NetworkStream Documentation
* Microsoft Path.Combine Documentation
* RFC 1123 Date Format Documentation

## License

Created for educational purposes as part of a Software Engineering Technology program.
