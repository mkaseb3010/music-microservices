This is a backend Java API microservice that is created using MongoDB and Neo4j Databases. We will also be using postman API to ensure a stable connection between the program and the server response with use of HTTP Status and server re-mapping. You will be able to add a song to your playlist or delete a song, like a song, just similar to alot of the features you may know from famous music applications such as Spotify and Apple Music.

**Required:**
  - Java version 1.8 is required.
  - Latest version of NoSQL (MongoDB).
  - Latest version of Neo4j.
  - Maven (preferably the latest version).
  - Postman API
  - mongodump, mongoimport, and mongosh (if not installed with MongoDB), you can download these tools here: https://www.mongodb.com/try/download/database-tools and for mongosh you can download here: https://www.mongodb.com/try/download/shell.

**Usage:**
Check this page on how to setup your Neo4j and MongoDB, it is important you set up Neo4j and MongoDB before trying to compile the microservices.
https://numbers-wonder-jnk.craft.me/QRwBOKoX0DVXpX

Ensure you are able to see maven properly setup in your IDE, you can run maven install -> maven clean -> maven test to setup maven, should you encounter any compiling issues run maven clean -> maven install -> maven test


When running the java code via eclipse (or an IDE of your choice), navigate to these 2 .java files:
  - profile-microservice -> src/main/java -> ProfileMicroserviceApplication.java
  - song-microservice -> src/main/java -> SongMicroserviceApplication.java
Right click on these files -> Run as -> run configurations -> in goals run the command "spring-boot:run" -> apply and ok

**For Windows Users:**
  - I recommend installing Git Bash for this step, you can also use Cygwin or WSL.
You will see a JSON file called MOCK_DATA and a shell scrip called import-songs-db
If MongoDB is setup properly you should be able to see localhost:27017 and a collection called eecs3311-test. Navigate to the songs folder inside.
Now when adding some data inside you will notice that ObjectId is not recognized by JSON but is required for MongoDB, so we have attached the shell script file that will automatically parse it to be recognized.

- run mongoimport --version -> mongosh --version -> mongodump --version (you should be able to see your version if all are installed properly)
- You will need to add the bin file for these tools into your systems environmental PATH.
- Open Git Bash
- Navigate to the directory where both of these files are located in
- run chmod +x import-songs-db.sh -> ./import-songs-db.sh
- If everything is setup properly you should be able to see a series of inputs added into MongoDB

**For macOS and Linux Users:**
Ensure MongoDB is live and running and that the MongoDB database tools are installed and added to your path variables
  - run export PATH=<path_to_mongodb_tools>/bin:$PATH
  - run mongod --dbpath <path_to_data_directory> to ensure MongoDB is live
  - chmod +x import-songs-db.sh -> ./import-songs-db.sh

**Postman API:**
This will be used to test the validity of the endpoints for the microservices

Example GET Command usage: http://localhost:3001/getSongTitleById/5d61728193528481fe5a3125
You should get this output printed:
{
    "path": "GET http://localhost:3001/getSongTitleById/5d61728193528481fe5a3125",
    "data": "Sanctuary",
    "status": "OK"
}

Similar if you want to delete a song

Example POST Command usage: for this you can navigate to the body section, make sure it is on JSON and raw, and you can add some data from MongoDB there, postman will expect 3 parameters as programmed -> (songName, songArtistFullName, songAlbum).

Example Song to add:
{
  "songName": "Blinding Lights",
  "songArtistFullName": "The Weeknd",
  "songAlbum": "After Hours"
}

Enter a a query key value
  - Key: Content-Type
  - Value: application/json
    
In the URL: http://localhost:3001/addSong/?Content-Type=application/json

Output:
{
    "path": "POST http://localhost:3001/addSong/?Content-Type=application/json",
    "data": {
        "songName": "Blinding Lights",
        "songArtistFullName": "The Weeknd",
        "songAlbum": "After Hours",
        "songAmountFavourites": 0,
        "id": "66d9d779996cde51281d4d92"
    },
    "status": "OK"
}

After refreshing MongoDB you will find the song added to your collection.


