Weather Activity Planner

A backend service that helps you discover the best activities based on weather conditions and location. The app fetches real-time weather data and suggests activities like skiing, surfing, hiking, or swimming depending on the current conditions.

Features

Real-time weather integration using Open-Meteo API
Activity recommendations based on weather conditions
City search and reverse geocoding
Configurable activity scoring with practical thresholds
Caching system to minimize API calls
REST API endpoints for easy integration
GraphQL support for flexible queries
Express.js server with comprehensive error handling

Tech Stack

TypeScript with strict mode enabled
Express.js for the REST API
Axios for HTTP requests
Open-Meteo for weather and geocoding data
Node.js runtime

Getting Started

Prerequisites

Node.js 14 or higher
npm or yarn

Installation

Clone or download the project

cd "back end"

Install dependencies

npm install

Build the project

npm run build

Running the Server

Start the development server

npm start

The server will run on http://localhost:3000

The API includes a health check endpoint at GET /health

API Endpoints

Get Weather Forecast

GET /weather?lat=51.5&lon=-0.1

Returns current and forecast weather data for the specified coordinates.

Search Cities

GET /cities/search?query=london

Search for cities by name. Returns latitude, longitude, and other city information.

Get Activity Recommendations

GET /recommendations?lat=51.5&lon=-0.1

Get personalized activity recommendations based on current weather at the specified location.

Health Check

GET /health

Simple health check endpoint. Returns status of the service.

How It Works

City Search

The app uses Open-Meteo's geocoding service to search for cities. When you search for a city, it returns matching results with coordinates.

Weather Fetching

Once you have coordinates, the weather endpoint fetches data from Open-Meteo's weather API. The data is cached for 30 minutes to avoid excessive API calls and improve performance.

Activity Scoring

The activity scoring system evaluates weather conditions against practical thresholds. For each activity, the system checks temperature, wind speed, and precipitation levels, then calculates a score from 0 to 100.

Scoring Thresholds

Skiing prefers very cold and snowy conditions
Surfing needs strong wind and moderate waves
Hiking works best in mild, dry weather
Swimming requires warm temperatures and low wind

Error Handling

The service includes comprehensive error handling for network issues, invalid coordinates, and API failures. Error messages are clear and include details about what went wrong.

Configuration

Thresholds for activity scoring are defined in the ActivityService. You can adjust these values to fine-tune recommendations:

Temperature thresholds: tempCold, tempVeryCold, tempHot
Wind thresholds: windModerate, windStrong
Precipitation thresholds: rainModerate, rainHeavy

API Response Format

Successful responses return JSON with the requested data. Error responses include an error message and relevant details.

Example weather response:

{
  "temperature": 15,
  "weatherCode": 2,
  "windSpeed": 12,
  "precipitation": 0,
  "isDaytime": true,
  "location": {
    "latitude": 51.5,
    "longitude": -0.1,
    "name": "London"
  }
}

Example activity recommendation:

{
  "activities": [
    {
      "name": "Hiking",
      "score": 85,
      "reason": "Perfect hiking weather with mild temperature and clear skies"
    },
    {
      "name": "Skiing",
      "score": 20,
      "reason": "Too warm for skiing today"
    }
  ]
}

Project Structure

src/services - Business logic for activities, weather, and cities
src/utils - Helper functions and API client configuration
src/types - TypeScript interfaces and types
src/graphql - GraphQL schema and resolvers
src/index.ts - Express server and route definitions

Testing

The project includes unit tests for individual services. Run tests with:

npm test

Tests cover weather fetching, activity scoring, city search, and error handling scenarios.

Future Improvements

GraphQL integration for flexible queries
Comprehensive test coverage with Jest
Database integration for user preferences
Activity history tracking
Personalized recommendations based on user history
Mobile app frontend

Contributing

Feel free to fork this project, make improvements, and submit pull requests. Areas for contribution include additional activity types, improved scoring algorithms, and extended test coverage.

Troubleshooting

Port already in use

If port 3000 is already in use, modify the PORT variable in src/index.ts

API rate limiting

Open-Meteo has rate limits. The caching system helps reduce requests, but if you hit limits, wait a few minutes before making new requests.

Coordinate format

Ensure coordinates are in decimal format: latitude between -90 and 90, longitude between -180 and 180

License

This project is open source and available for personal and commercial use.

Questions

For issues, questions, or suggestions, feel free to open an issue or contact the project maintainers.
