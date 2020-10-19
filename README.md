# FileManagement

Node Application for file upload and download (with compression).

## modules used 

Nodejs, Express, Sequelize, Mullter

## .env file

PORT=3000 (Port that will be used for the server)
ENV=test (test or development if test the auth middleware will be ignored so uploads or downloads could be done without authentication).

## Config file 

Configuration file is separated to 3 different parts :

1 - Applications : [
    {
        name of the application,
        id of the application,
        Absolute path where we will store the file uploaded for the application (the folders should be set up manualy except the application forlder)
        for ex : /home/xox/test/myHSE/ (/home/xox/test, need to be created manualy), but the (/myHSE it's handled by the app, if it's not created manually the application will create it).
    }
]

2 - settings : {
    maxFileUpload : is the max number that a user can upload in a single request,
    usersApi : the URL for the users Api (used for check user token during upload and download).
}

3 - database_settings : {
    dbName : database name (should be created manually).
    username : username that sequelize will use to connect to database.
    password : password that sequelize will use to connect to database.ee
    host : Url for the database.
    dialect : dialect that sequelize will us to talk with the database and       construct it's query's.
}

## Routes All Routes should be given a header {token : "Token content"} for authentication purposes

### POST : "/upload/:app" for example /upload/1 to upload to application 1 storage.
    Content : "file": an array of files to upload, should be form-data content (Multer can only handle form-data content).
    Response : {
        newFileName : fileName of the new uploaded file *(should be storage to be given in the download section).
    }

### POST : "/download"
    Content : {
        appId : application id from which we want to download,
        fileName : FileName we want to download (response of the upload section)
    }
