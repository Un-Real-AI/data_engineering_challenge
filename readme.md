# Engineering Challenge - 42Hacks

Welcome to the engineering challenge! Your goal is to extract, transform, and make data available to other users through an API.

## Challenge Objective

The objective of this challenge is to find the closest airport for a list of 100,000 users. You will retrieve user location data from a provided REST API and match each user to their nearest airport from a dataset of registered airports.

## Steps to Complete the Challenge

### 1. Retrieve User Locations
You can access the user location data (containing user ID, longitude, and latitude) from the following [REST API](https://sccr8pgns0.execute-api.us-east-1.amazonaws.com/dev/locations). Each data point can be retrieved using the following syntax:

```python
requests.get('https://sccr8pgns0.execute-api.us-east-1.amazonaws.com/dev/locations/' + str(user_id)).json()
```
<p align="center">
  <img src="./assets/airport_324754607.jpeg" />
</p>

### 2. Retrieve Airport Data
Use the dataset from the [OurAirports](https://ourairports.com/) webpage. The dataset, named **airports.csv**, contains the following schema:
- "id"
- "ident"
- "type"
- "name"
- "latitude_deg"
- "longitude_deg"
- "elevation_ft"
- "continent"
- "iso_country"
- "iso_region"
- "municipality"
- "scheduled_service"
- "gps_code"
- "iata_code"
- "local_code"
- "home_link"
- "wikipedia_link"
- "keywords"

### 3. Create a Filtered Dataset
Generate a CSV file named **airports_w_wiki.csv** containing only the airports that have a Wikipedia page. This file must be uploaded to your GitHub repository.

### 4. Build the API
Develop a REST API with the following functionality:
1. Retrieve the closest airport for a user: 
   - Endpoint: **/nearest_airports/<user_id>**
   - Response: JSON containing the "airport_id" of the nearest airport.
2. Retrieve the Wikipedia page for the closest airport:
   - Endpoint: **/nearest_airports_wikipedia/<user_id>**
   - Response: JSON containing the "wikipedia_page" URL of the nearest airport.

### 5. Database Integration
Create a database that stores 100,000 user points with fields "user_id" and "airport_id". Ensure your API queries this database efficiently.

## Deliverables
1. **airports_w_wiki.csv**: Upload this file to your GitHub repository.
2. **REST API**: The API should fulfill the endpoints described above.

## Evaluation Criteria
Your solution will be evaluated based on the accuracy and efficiency of your code, using a provided **eval.py** script. Ensure your API can retrieve data with the following commands:

```python
requests.get(BASE_PATH + '/nearest_airports/<user_id>').json()["airport_id"]
```
```python
requests.get(BASE_PATH + '/nearest_airports_wikipedia/<user_id>').json()["wikipedia_page"]
```

### Scoring Matrix
| Challenge | Excellent | Good | Satisfactory | Insufficient |
|-------------------------------|-------------|---------------|--------------|--------------------------|
| Compute list of airports with Wikipedia page | **10 points** <br> - All the airport ids with Wikipedia page are in the script <br> - The code is clean and efficient | **6 points** <br> - All the airport ids with Wikipedia page are in the script <br> - The code is not efficient or easy to read | **4 points** <br> - The list of airports is incomplete or includes airports without Wikipedia page <br> - The code is not efficient | **0 points** <br> - The solution is wrong |
| API retrieving the closest airport for each user | **50 points** <br> - All the airport ids correspond to the closest airport <br> - The code is clean and efficient | **40 points** <br> - All the airport ids correspond to the closest airport <br> - The code is not efficient or easy to read | **20 points** <br> - The list of airports is incomplete or includes wrong airport ids <br> - The code is not efficient | **0 points** <br> - The solution is wrong |
| API retrieving the Wikipedia page for the user's closest airport | **40 points** <br> - All the airport Wikipedia pages correspond to the closest airport <br> - The code is clean and efficient | **30 points** <br> - All the airport ids correspond to the closest airport <br> - The code is not efficient or easy to read | **15 points** <br> - The list of airports is incomplete or includes wrong airport ids <br> - The code is not efficient | **0 points** <br> - The solution is wrong |

## Hints
- Remember to consider the spherical nature of geographic coordinates. Use the [Haversine formula](https://en.wikipedia.org/wiki/Haversine_formula) for distance calculations.
- Parallelize your code to improve performance.
- As the API has a limited reading capacity limit your parallel requests such that you perform around 60 reads per second.
- Program your script to handle errors in case you receive a bad http response. In such a case you can speed your code to handle 344 reads per second.
- Handle errors gracefully in case of bad HTTP responses.
- Use inner joins to efficiently retrieve data.

## Submission
When finished, send an email to nicolas@42hacks.com with a link to your GitHub repository, which should include the API path in the README and the **airports_w_wiki.csv** file attached. Good luck!
