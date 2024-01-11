# APIs
- API stands for application programming interface, which is a set of definitions and protocols for building and integrating application software.
- Set of Definitions how to interact with an Interface
- provide datam functionality or 3rd party services
- hide implementation details
- API is like the middleware between client and server
- client requests are reponded to on a one-to-one basis (one response per request)
- Common API Strucktures
  - SOAP Simpel Object Acces Protocol
    - Works with XML, considert outdated
  - REST Representational State Transfer, achitectural style
    - for HTTP Protocols and verbs(GET, POST, PUT, DELETE), mostly JSON, CRUD compatible
    - RESTful API comunication via different paths a.k.a. Endpoints
   - [HTTP request methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

### Interface 
- is a device or system the unrelated entities use to interact
- An interface is a named collection of method definitions, it can also include constant declarations
### URLs
    https://myproject.org/users?country=DE&lang=EN#contact
    Protocol    Domain    Path   Query            Fragment
  
  - GraphQL
    - uses format similar to JSON
    - singel Endpoint that expects a querry wich details how the response should be structured
    - highly customizable result with no superflous data


## Fetching Data
