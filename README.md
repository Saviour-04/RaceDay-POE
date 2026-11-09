# RaceDay Event Management System - Part 3
name :saviour mkhatshwa
student number :st10489983

## 📋 Project Overview
RaceDay is a full-stack web-based event management system designed for the South African road running, walking, and cycling community. This platform allows Event Organisers to create and manage events, while Participants can browse, enter events, and track their performance. 

This repository contains the complete solution built across three parts:
*   **Part 1:** System Planning (ERD, API Endpoint Plan, SQL Database Script)
*   **Part 2:** RESTful API built with ASP.NET Core Web API (C#) and Entity Framework Core.
*   **Part 3:** MVC Web Application consuming the API, Azure Blob Storage integration, and Docker containerisation.

## 👥 User Roles
1.  **Organiser:** Can create events, upload banner images (stored in Azure), view enrolments, and capture results.
2.  **Participant:** Can browse upcoming events, enrol in events, and view their personal results.

## 🚀 Setup & Run Instructions

### Prerequisites
*   .NET 8.0 SDK
*   SQL Server & SQL Server Management Studio (SSMS)
*   Docker Desktop
*   Azurite (or an active Azure Storage Account)

### Database Setup
1. Open SSMS and run the `RaceDay_Database.sql` script located in the `/docs` folder.
2. This will create the `RaceDayDB` database, tables, and seed data.

### Running the API (Part 2)
1. Open `RaceDay API.sln` in Visual Studio.
2. Ensure the `appsettings.json` connection string points to your SQL Server.
3. Ensure your Azure Storage connection string is set in `appsettings.json` (or use `UseDevelopmentStorage=true` for Azurite).
4. Press **F5** to run the API. Note the port number (e.g., `https://localhost:7220`).

### Running the MVC App (Part 3)
1. Open `RaceDayMVC.sln` in Visual Studio.
2. Check `Program.cs` to ensure the `client.BaseAddress` points to your API's port.
3. Press **F5** to run the MVC application.

### 🐳 Docker Setup
To run the MVC application inside a Docker container:
1. Ensure Docker Desktop is running.
2. Open a terminal in the `RaceDayMVC` folder.
3. Build the Docker image:
   ```bash
   docker build -t racedaymvc -f Dockerfile .


  Run the container:

bash
docker run -d -p 8080:80 --name raceday-container racedaymvc
Access the app at http://localhost:8080.

☁️ Azure Blob Storage Integration
The application uses Azure Blob Storage to handle event banner uploads.

The MVC frontend sends the image to the API using MultipartFormDataContent.

The API receives the file, uploads it to the Azure Blob container (event-banners), and saves the generated URL to the SQL database.

The MVC app then reads this URL from the database to display the event banner.

🔄 CI/CD Pipeline
This project uses GitHub Actions for Continuous Integration.
https://github.com/[YOUR-GITHUB-USERNAME]/[YOUR-REPO-NAME]/actions/workflows/dotnet.yml/badge.svg

🎥 Video Presentation
link :

Video Covers:

Full application walkthrough (Organiser & Participant).

Azure Blob Storage image upload demonstration.

Docker containerisation setup.

Code structure explanation.

