# Project Name
Hotel Management App

# Frameworks and Language Used
**Spring Boot** 3.1.4
**Java** 17
**Maven** 3.8.1

# Data Flow


_**Controller:**_ The controller has endpoints for adding a room or list of rooms, getting all rooms, getting a room by its ID, getting all rooms by price, get all rooms available and less than given price, get all rooms available or less than given price, get all rooms available or having ac(sorted by price) and delete hotel by id. 

The @PostMapping annotation is used for the room or rooms endpoint to handle HTTP POST requests with a JSON request body containing a room or list of rooms  object. 
```java
@PostMapping("room")
    public String addRoom(@RequestBody Room newRoom)
    {
        return roomService.addRoom(newRoom);
    }

    //add multiple rooms at once :
    @PostMapping("rooms")
    public String addRooms(@RequestBody List<Room> newRooms)
    {
        return roomService.addRooms(newRooms);
    }
```

The @GetMapping annotation is used for the rooms, rooms/id/{id}, rooms/price/{price}, rooms/price/{price}/and/available, rooms/price/{price}/or/available, rooms/AC/or/available endpoints to handle HTTP GET requests with and without a path variable for the room ID or room price, respectively. The @PathVariable annotation is used to extract the room ID or price from the request URL and pass it to the required method.
```java
@GetMapping("rooms")
    public List<Room> getRooms()
    {
        return roomService.getRooms();
    }

    @GetMapping("rooms/id/{id}")
    public Room getRoomById(@PathVariable Integer id)
    {
        return roomService.getRoomById(id);
    }

    @GetMapping("rooms/price/{price}")
    public List<Room> getRoomByPrice(@PathVariable double price)
    {
        return roomService.getRoomByPrice(price);
    }


    @GetMapping("rooms/price/{price}/and/available")
    public List<Room> getAvailableRoomsBelowPrice(@PathVariable double price)
    {
        return roomService.getAvailableRoomsBelowPrice(price);
    }


    @GetMapping("rooms/price/{price}/or/available")
    public List<Room> getAvailableRoomsOrBelowPrice(@PathVariable double price)
    {
        return roomService.getAvailableRoomsOrBelowPrice(price);
    }

    @GetMapping("rooms/AC/or/available")
    public List<Room> getAvailableRoomsOrAcSortedByPrice()
    {
        return roomService.getAvailableRoomsOrAcSortedByPrice();
    }
```

The @DeleteMapping annotation is used for the room/ids endpoint to handle HTTP DELETE requests with a list of ids as a requestbody.
```java
@DeleteMapping("rooms/ids")
    public String removeRoomsByIds(@RequestBody List<Integer> ids)
    {
        return roomService.removeRooms(ids);
    }
```

The controller class also has an autowired instance of the RoomService interface to handle business logic for the Hotel Management App.

This implementation demonstrates a basic setup for a REST API controller in Spring Boot, but it can be expanded upon and customized based on specific requirements for the Hotel Management App.

In the application.properties all the text required for connection with h2 database are written.
```java
spring.datasource.url=jdbc:h2:mem:h2db
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=ina728mg
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect



spring.h2.console.enabled=true

spring.jpa.properties.hibernate.show_sql=true
spring.jpa.properties.hibernate.use_sql_comments=true
spring.jpa.properties.hibernate.format_sql=true
```

_**Services**:_ The services layer contains the business logic of the application. It receives requests from the controller, performs necessary computations or data manipulations, and interacts with the repository layer to access data.

_**Repository:**_ The repository layer is responsible for interacting with the database. It uses Spring Data JPA to perform CRUD (create, read, update, delete) operations on entities.

# Database Structure Used
I have used h2 as DataBase

# Project Summary
In this project i have create different endpoints and created custom finders as per required.
