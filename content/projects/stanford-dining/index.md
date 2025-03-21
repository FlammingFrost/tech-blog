---
title: Find Your Disher @ Stanford Dining
seo_title: Find Your Disher @ Stanford Dining
summary: A AI-powered ETL system to help you find your disher at Stanford Dining.
description: Obtain data through web scraping, clean transform data; Build AI chatbot to automatically interpret query, generate SQL query, and give response. Deployed on Google Cloud Run through FastAPI.
slug: dining-hall-explorer
author: FlammingFrost

draft: false
date: 2025-03-19
lastmod: 
expiryDate: 
publishDate: 

feature_image: preview.png
feature_image_alt: 

project types: 
    - Personal

techstack:
    - FastAPI
    - Docker
    - SQLite
    - AI chatbot
live_url: https://fastapi-app-902489793845.us-central1.run.app/
source_url: https://github.com/FlammingFrost/Dining-Hall-Explorer
---

# Find Your Dish @ Stanford Dining: An AI-Powered ETL System for Smarter Dining Choices

> Try it out: [Find Your Dish @ Stanford Dining](https://fastapi-app-902489793845.us-central1.run.app/)

### Overview

Find Your Dish @ Stanford Dining is an innovative AI-powered ETL system designed to enhance the dining experience at Stanford University. The system automates data extraction, transformation, and loading (ETL) to provide students and faculty with real-time, structured information about daily menu offerings across different dining halls. By leveraging web scraping techniques and AI-driven data processing, the system ensures up-to-date dining information. (*But not accurated because the website is not always accurate*)

In addition to structured menu data, the project integrates an AI chatbot that enables users to search for specific dishes, filter dietary preferences, and receive personalized meal recommendations. The chatbot translates natural language queries into structured SQL database queries, returning relevant results in a conversational format.

### AI-Powered ETL Pipeline

The system follows a multi-stage ETL pipeline that consists of:
	1.	**Data Extraction (E)** – Web Scraping
	•	Automated web scraping of Stanford Dining’s online menu using Selenium.
	•	Extracts details such as dish names, ingredients, allergens, etc.
	•	Ensures data freshness by running scheduled updates.
	2.	**Data Transformation (T)** – AI-Powered Cleaning & Structuring
	•	AI-assisted text processing to extract structured information from unstructured menu data.
  •	Cleans and standardizes dish names, ingredients, and descriptions. Identifies cuisine type and specific meat parts to match user preferences.
	•	SQL database structuring using SQLite for fast query execution and retrieval.
	3.	**Data Loading (L)** – Storage & AI Querying
	•	Stores structured data in a relational SQLite database.
	•	AI-powered chatbot translates natural language queries into optimized SQL queries to fetch relevant dining options.

### Deployment & Scalability

The system is built with FastAPI, packaged in a Docker container, and deployed on Google Cloud Run for scalability and cost-efficiency. Key components include:
	•	FastAPI Backend: Handles API requests, chatbot logic, and query execution.
	•	Docker Containerization: Ensures portability and consistency across different environments.
  •	Google Cloud Run: Serverless deployment for automatic scaling and cost-effective operation.

With AI-driven insights, intelligent query processing, and a scalable cloud-based infrastructure, **Find Your Dish @ Stanford Dining** \*revolutionizes\* the way students interact with their dining options, making meal selection more convenient, personalized, and accessible.