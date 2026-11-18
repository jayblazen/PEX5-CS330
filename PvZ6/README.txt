CS 330
Fall 2025

From PvZ folder
To complile 
javac -d out $(Get-ChildItem -Recurse -Filter *.java | Select-Object -ExpandProperty FullName)

To run 
java -cp out core.PvZ6






Name: Ayden Woodhead
Documentation Statement:
    I used https://www.w3schools.com/java to refrenece java docs, math functions and example
    I used https://github.com/jayblazen/ThunderRaptor as a refrenece to my game math functions which help with sundrops and organization structure 
    I used https://www.geeksforgeeks.org/java/java-directories-programs/ and https://www.youtube.com/watch?v=5Srjptsbd4Y&t=2 to help with the folders and outputing to an out folders
    


PEXA- problems to fix:
Problem A: sun Collected is global variable
    Add a level manager class that controls zombies spawns, sun amount, starting plants etc

Problem B: PeaShooter shoot indiscriminately
    2 good ways, already have a generic collision system so could do a detection Collision box or can use a observer system from 
    spawning a zombie -> update lawn row and plants.

Problem C: Zombies don’t eat plants
    Add collision box and collision manager. Already developed generic in DinoWorld to copy over to here

Problem D: Peas don’t damage zombies
    Add collision box and collision manager 



PEXB- how it was fixed:
problem A: half fixed- moved to lawn to handle sun collection but still global var- easy fix if needed

Problem B: Peashooters no longer shoot all the time
    Game keeps a list of peashooters observing zombie changes. When a zombie is added or removed, Game notifies each registered peashooter, which updates whether a living zombie is ahead in its row

Problem C: Zombies can eat plants
    Game finds the closest plant ahead of each zombie in the same row and passes it to the zombie's update method. 
    Zombie compares its collision shape with the plant's collision shape; while they overlap, it stops moving and eats the plant

Problem D: Peas damage zombies
    Plants, zombies, and peas have collision shapes with layers that specify which types they can detect. 
    Game adds living zombies to the CollisionSystem, updates each projectile, and checks it for a collision. On a hit, the zombie takes the pea's damage and the pea is removed. 

Design patterns and organization:
    GardenManager uses the Singleton pattern: its constructor is private and getInstance() provides the shared manager used by Game
    Problem B uses the Observer pattern: Game is the subject, and placed peashooters are observers notified when the zombie collection changes
    SeedPacketUI uses a factory-style approach by accepting a Supplier that creates a Plant, so the packet UI can create different plant types without being coupled to each concrete plant class
    CollisionSystem also centralizes collision checks instead of having projectiles perform those checks themselves


other notes:
    I tried to make this way more modular, I tested to make sure things work with more rows to prevents hard coding and moved alot of constants to classes
    also redid the UI to take in only the plant to and build the button based off the plant data
    still didnt get to finish zombie spawner and wave stuff since I got lazy and didnt finish this game

known bugs:
    The grid lines disappear when the pea shoots-- idk why probably with how I ordered the draw- fun part it comes back when placing a plant
