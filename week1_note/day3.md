    # What is HTTP? (Hypertext transfer protocol)
    -> application-layer protocol designed for fetching resources, such as HTML documents, images, and videos (Là nền tảng của data exchange trên web)

    -> Hoạt động trên client-server model, define data exchange
    
    # Several key characteristics:
        Đơn giản và dễ đọc: HTTP messages được thiết kế để con người đọc và hiểu, đơn giản việc testing và debugging for developers.

        Có thể mở rộng ra: 
            HTTP headers allow the protocol to be easily extended, 
            Enables features such as caching, authentication, and the relaxation of origin constraints (nới lỏng các ràng buộc về nguồn gốc)

        Stateless but not Sessionless (ko có trạng thái nhưng có phiên):    
            HTTP is stateless (no automatic link between two successive requests on the same connection), 
            HTTP cookies allow the creation of stateful sessions, enabling contexts to persist across multiple requests (Cho phép tạo các phiên có trạng thái, cho phép 1 vài ngữ cảnh tồn tại qua nhiều yêu cầu)
        
        Reliable Transport:
            relies on a reliable transport layer (dựa vào lớp truyền tải đáng tin cậy)
            typically uses TCP or a TLS-encrypted TCP connection.


    # Requests and responses:
    -> Communication in HTTP occurs by exchanging individual messages rather than a continuous stream of data.

    Client: 
        The browser is always the entity that initiates the request; the server never initiates the request itself
        Để hiển thị (display): browser gửi initial request cho HTML document, parse nó (phân tích cú pháp) sau đó sends subsequent requests for sub-resources
    
    Server:
        handles the request and provides an answer called the response
        A server may appear as a single machine, but it often consists of a collection of servers sharing the load or generating content on demand.

    Proxies:
     Giữa client và server có thể có nhiều application-layer -> gọi là proxies
     Những cái entities này can handle various functions, including caching, filtering, load balancing, authentication, and logging


    # HTTP messages
    -> HTTP messages are the specific packets of data exchanged between client and server

    # There are 2 types of HTTP messages:
        1. Requests A request:
            HTTP Method:
                Usually a verb or a noun defining the desired operation.
            Path:
                The URL of the resource, stripped of the protocol, domain, and port.
            Version:
                The version of the HTTP protocol 
            Headers:
                Optional fields
            Body:
                A component used for some methods  to contain the resource being sent
        2. Responses A response
            Version:
                The version of the HTTP protocol the server follows
            Status Code:
                A code indicating if the request was successful or not (404, error)
            Status Message:
                A short, non-authoritative description of the status code.
            Headers:
                Optional fields
            Body:
                Optionally contains the fetched resource

    # GET method:
        used to request a representation of a specified resource
        Mục đích là để retrieve data
        Characteristics:
            ◦ Safe: Yes.
            ◦ Idempotent: Yes.
            ◦ Cacheable: Yes.

    # POST method:
        submits an entity to a specified resource
        Mục đích là để send data to the server, often resulting in a change in state or side effects on the server
        Characteristics:
            ◦ Safe: No.
            ◦ Idempotent: No.
            ◦ Cacheable: Conditional. While generally not cacheable, POST can be cached if the response explicitly includes freshness information and a matching Content-Location header


    RESPOND STATUS:
    # 200-OK:
        This is the standard response for a successful HTTP request. The specific meaning of "success" depends on the request method used:
            • GET: The resource has been fetched and is included in the message body.
            • HEAD: Headers are returned without the message body.
            • PUT or POST: The message body contains the result of the action.
            • TRACE: The message body contains the request exactly as the server received it.

    # 301-Moved Permanently
        This redirection code indicates that the URL of the requested resource has been changed permanently.
            • The new URL is provided in the response.
            • Future requests should use this new URL.
    
    # 401 Unauthorized
        This client error indicates that the request has not been applied because it lacks valid authentication credentials.
            • Meaning: Although standardly named "Unauthorized", it semantically means "unauthenticated".
            • Action Required: The client must authenticate itself (e.g., log in) to receive the requested response.
    
    # 403 Forbidden
        This client error indicates that the server understands the request but refuses to authorize it.
            • Meaning: The client does not have access rights to the content.
            • Distinction from 401: Unlike the 401 status, the client's identity is known to the server, but they simply lack the necessary permissions
        
    # 404 Not Found
        This is likely the most well-known response code on the web. It indicates that the server cannot find the requested resource.
            • Browsers: Typically means the URL is not recognized.
            • APIs: Can mean the endpoint is valid, but the specific resource does not exist.
            • Security Use: Servers may sometimes send a 404 instead of a 403 Forbidden to hide the existence of a resource from an unauthorized client.

    # 500 Internal Server Error
            This is a generic server error response.
            • Meaning: The server has encountered a situation it does not know how to handle.
            • Usage: It is a "catch-all" code used when no more specific 5XX status code is suitable.

Day3/week1