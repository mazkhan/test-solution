To run the program
1) Go to the root directory of the project and run "gradle bootRun" or "gradlew bootRun"
2) Import as gradle project in your favourite IDE and run as spring project

To run tests
1) Go to the root directory of the project and run "gradle clean test" or "gradlew clean test"
2) Run as Junit tests in the IDE

Design decisions

1. Call to the hadoop service is asynchronous as the hadoop service is a long running service
2. In case of failure of call to hadoop datalake service it is retried to a maximum of 4 times, which gives it a 93.75% chance of success as each request to the datalake has a chance of 50% failure
3. If all 4 retries fail then no further action is taken as a later recovery process(using queues or such) is out of the scope of this simple implementation and this way our service can function even in case of failure of an external service.
4. Due to the simplicity of the data models the same model classes are used for requests and responses.
5. Rest endpoints have been reused from the client implementation
6. Body md5 signature is sent in the header portion as the header object seems to contain attributes of the body. It is not sent as a http request header as it is not the md5 hash of the whole body

Developed using

Gradle 6.4
openjdk version "11.0.8" 2020-07-14

Tested on Java 8


Sample usage
Please use a client like postman 



POSTDATA
url:  http://localhost:8090/dataserver/pushdata

header:
Content-Type    :   application/json

request body:

{
    "dataHeader": {
        "name": "TSLA-USDGBP-11Y",
        "blockType": "BLOCKTYPEB",
        "bodyMD5Signature": "cecfd3953783df706878aaec2c22aa70"
    },
    "dataBody": {
        "dataBody": "AKCp5fU4WNWKBVvhXsbNhqk33tawri9iJUkA5o4A6YqpwvAoYjajVw8xdEw6r9796h1wEp29D"
    }
}


GET DATA
url : http://localhost:8090/dataserver/data/BLOCKTYPEB


PATCH DATA
url: http://localhost:8090/dataserver/update/TSLA-USDGBP-10Y/BLOCKTYPEA

(case of blocktype is important)








To run the program
1) Go to the root directory of the project and run "gradle bootRun" or "gradlew bootRun"
2) Import as gradle project in your favourite IDE and run as spring project

To run tests
1) Go to the root directory of the project and run "gradle clean test" or "gradlew clean test"
2) Run as Junit tests in the IDE

Design decisions

1. Call to the hadoop service is asynchronous as the hadoop service is a long running service
2. In case of failure of call to hadoop datalake service it is retried to a maximum of 4 times, which gives it a 93.75% chance of success as each request to the datalake has a chance of 50% failure
3. If all 4 retries fail then no further action is taken as later recovery process is out of the scope of this simple implementation
4. Due to the simplicity of the data models the same model classes are used for requests and responses.
5. Rest endpoints have been reused from the client implementation
6. Body md5 signature is sent in the header portion as the header object seems to contain attributes of the body. It is not sent as a http request header as it is not the md5 hash of the whole body


Sample usage
Please use a client like postman 



POSTDATA
url:  http://localhost:8090/dataserver/pushdata

header:
Content-Type    :   application/json

request body:

{
    "dataHeader": {
        "name": "TSLA-USDGBP-11Y",
        "blockType": "BLOCKTYPEB",
        "bodyMD5Signature": "cecfd3953783df706878aaec2c22aa70"
    },
    "dataBody": {
        "dataBody": "AKCp5fU4WNWKBVvhXsbNhqk33tawri9iJUkA5o4A6YqpwvAoYjajVw8xdEw6r9796h1wEp29D"
    }
}


GET DATA
url : http://localhost:8090/dataserver/data/BLOCKTYPEB


PATCH DATA
url: http://localhost:8090/dataserver/update/TSLA-USDGBP-10Y/BLOCKTYPEA

(case of blocktype is important)






