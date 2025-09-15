# FS_AbhishekYadav
# High Overview Description : (Student Commute Optimizer - Ride Sharing App) 
      A full-stack app that helps students carpool by matching similar commute routes. Users enter home and destination, see nearby commuters on a map, and chat anonymously in real-time. It ensures privacy with unique usernames and uses route matching to optimize shared       rides,saving money and time, reducing traffic and pollution,  cutting commute costs.<br>

Keeping It Simple, I am going to provide the approach for this project with high overview structure and planning.
---
# FRONTEND

      - To optimize it better we will use REACT VITE or Angular instead of relying on traditional HTML and CSS.  
      - Flow of the app will be:  
        - A **LogIn and Register Page which will send user details to the backend authentication and create user endpoint API which returns a unique username (username should be random to keep anonymity) to the frontend to display and stored in global state                      (useContext or REDUX).  
        - Store user **JWT token** and other credentials excluding password in some store/slice.  
        - An `/route` or `/search` page (routes) which contains a form for input source and **input destination** and a Submit button.  
        - For input locations we will use address autocomplete APIs of Leaflet or any other autocomplete providing host such that user is not able to enter any non-existing address.  
        - **Validations of inputs must also be taken care of such as required field etc.  
        - If possible we can allow the page to get user current location using browser navigation API for latitude and longitude coordinates.  
        - The form with source and destination is then submitted through backend route generating API for route processing.  
        - The backend provides best route with minimum obstruction which the frontend shows.  
        - For showing routes we will use Mapbox GL with pop-up marker showing location of user source and destination inputs.  
        - The pop-up marker will act as a button with username as tooltip (anonymous names) which will serve as opening a real-time chat with users nearby.  
        - When the map is displayed we will also show nearby pop-ups which fall within a certain threshold radius for sharing rides.  
        - An **Error Page** for showing errors. If hit wrong URL or failed to fetch from APIs etc.  
---

    #   A basic flow diagram:<br>
    [Start / Open App]
            |
    [Login / Register] ---→ [Generate Unique Username]
            |
    [Home Screen]
       ├── Enter Home Location
       ├── Enter Destination (School/College)
       └── Save & Submit
            |
    [Map Screen]
       ├── Shows route from Home → Destination
       ├── Fetches nearby students on similar routes
       └── Displays students as anonymous icons
            |
    [Student Icon Click]
       ├── View basic profile (Anonymous username, same route)
       └── Option: "Chat"
            |
    [Chat Screen]
       ├── One-to-one messaging
       ├── Anonymous identity preserved
       └── Option: "Back to Map"
            |
  [End / Logout]
---
 # Backend

      - We will use **Node.js** as runtime environment for running our JavaScript and Express for routing and other stuff, integrated with databases like MongoDB (for document collection) or MySQLi (if needed to store in tables).  
      - Flow of the backend will be:  
        - Express and Node setup with configured ports, env, databases.  
        - Routes to create endpoints for different functions.  
        - Middlewares for validating details before we hit actual endpoints.  
        - Create and verify endpoints using JWT tokens.  
        - Using MapBox API to create an optimized route and send it to frontend for display.  
        - Database having tables or collections storing essential data such as user unique anonymous usernames, locations.  
        - An endpoint where we will write overlapping route logic by comparing routes of different users nearby provided by nearby users frontend MapBox API, a basic approach can be calculating how much distance is overlapping in same direction by all users and rank them for particular user and return filtered markers for nearby best users.  
        - For real-time chat service we will use WebSockets (Socket.io) with one-to-one connections only.  
        - Store previous chats in database for fetching it later, save and return to frontend only few messages by deleting old messages using a queue or last-in-first-out based data structure.  
---
#   A basic flow diagram:<br>
    [Frontend Request]  
            |  
    [API Gateway / Server]  
            |  
    [Authentication Service]  
       ├── Validate Login/Register  
       └── Generate Unique Anonymous Username  
            |  
    [Student Database]  
       ├── Store user credentials (securely)  
       ├── Store unique anonymous username  
       └── Store location & destination  
            |  
    [Route Matching Engine]  
       ├── Get student's route (from Maps API)  
       ├── Compare with existing student routes  
       ├── Calculate overlap/proximity  
       └── Generate match suggestions  
            |   
    [Matchmaking Service]  
       ├── Return matched student IDs (anonymous usernames)  
       ├── Attach approximate location markers  
       └── Send back to frontend  
            |  
    [Chat Service (WebSocket / Realtime)]  
       ├── Establish 1:1 chat connection  
       ├── Route messages securely  
       └── Store chat logs (optional)  
            |  
    [Response → Frontend]
          
      
