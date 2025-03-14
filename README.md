
# Multithreaded Proxy Server
1. Built a proxy server that handles multiple client requests at the same time, with optional caching of server responses. </br>
2. Managed concurrent requests using semaphores, locks, and an HTTP parser. Implemented an LRU cache, linked lists, and custom structs to achieve efficient multi-threading and prevent race conditions. </br>
3. Enabled parallel processing of client requests, allowing the system to handle numerous requests simultaneously. </br>

## Tech used:-
1. Socket programming- the proxy server communicates with clients and web servers using sockets.</br>
2. Multithreading- Multiple clients can connect to the proxy server simultaneously. Each client request is handled in a separate thread to allow concurrent processing. </br>
3. Caching- the server can cache responses from web servers to serve future requests without contacting the server again. This reduces response time.</br>

## Files
1. proxy_parse.c: This file focus on parsing HTTP requests, extracting information such as the host, port, path, and HTTP version.</br>
2. proxy_server_with_cache.c: This is the core implementation of the proxy server, which includes handling client requests, managing cache (using an LRU mechanism), and ensuring multithreading with proper synchronization mechanisms (like locks and semaphores).</br>
The server creates a socket and listens on a specific port (8080 by default). It accepts connections from clients and forwards their requests to the target server. Once the server responds, the proxy server returns the response to the client.</br>

## Workflow:
1. Client connects: A client sends an HTTP request to the proxy server.
2. Request Parsing: The proxy parses the HTTP request (using the proxy_parse function).
3. Cache Check: The proxy checks if the response is already in the cache:</br>
If the response is in the cache, the proxy serves the cached response.</br>
If not, the proxy forwards the request to the target server.</br>
4. Forwarding and Response: The proxy sends the client request to the target server and retrieves the response.
5. Caching: If caching is enabled and the response is cacheable, the proxy stores the response in the cache.
6. Response to Client: The proxy sends the response back to the client.
7. Multithreading: This process is handled concurrently for multiple clients using threads.
8. Concurrency Control:</br>
The use of semaphores and locks ensures that multiple clients can access the server concurrently without causing inconsistencies. For example:</br>
Cache Locking: Access to the cache is controlled by a mutex lock to prevent race conditions where multiple threads try to modify the cache at the same time.</br>
Request Handling: Each client request is handled in a separate thread, allowing the server to handle multiple clients concurrently.</br>
10. LRU Cache Implementation:
find(char* url): This function looks for the requested URL in the cache.</br>
add_cache_element(char* data, int size, char* url): Adds a new element to the cache. If the cache is full, it removes the least recently used element.</br>
remove_cache_element(): Removes the least recently used cache element to free up space when needed.</br>

## How to run
1. Install cmake extension in vs code</br>
2. Run run command "make" in terminal</br>
3. Turn on the proxy server by command "./proxy 8080"</br>
