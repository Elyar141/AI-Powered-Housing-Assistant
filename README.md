# AI-Powered Housing Assistant

An automated housing search and application system built with n8n that helps users find apartments and automatically generate personalized application letters.

## Overview

This system consists of three main components:

1. **Daily Web Scraper for Gewobag** - Collects apartment listings daily from Gewobag
2. **Daily Web Scraper for eBay** - Collects apartment listings daily from eBay Kleinanzeigen
3. **AI-Powered Housing Agent via Telegram** - A conversational interface for users to search listings and generate application letters

The system leverages AI to:
- Understand natural language search queries
- Filter housing listings based on user preferences
- Generate personalized application letters tailored to specific listings and user profiles

## Features

- **Automated daily scraping** from multiple sources
- **Deduplication** to prevent duplicate listings
- **Conversational interface** via Telegram
- **Natural language search** for properties (e.g., "find me a 2-room apartment in Mitte under 1000€")
- **Intelligent filtering** based on price, location, size, and other criteria
- **Auto-generated application letters** customized to both the listing details and user's personal information

## Prerequisites

- [n8n](https://n8n.io/) instance
- [NocoDB](https://nocodb.com/) account for database
- [Telegram Bot](https://core.telegram.org/bots#how-do-i-create-a-bot) for user interface
- [Apify](https://apify.com/) account for web scraping
- [OpenAI API](https://openai.com/api/) access for AI capabilities

## Installation

1. Import the workflow JSON file into your n8n instance
2. Set up the required credentials:
   - NocoDB API token
   - Telegram Bot token
   - Apify API token
   - OpenAI API key
3. Configure the placeholders in the workflow:
   - Replace `YOUR_WORKSPACE_ID`, `YOUR_PROJECT_ID`, and `YOUR_TABLE_ID` with your NocoDB details
   - Replace `YOUR_ACTOR_TASK_ID` with your Apify actor task IDs
   - Replace `YOUR_APIFY_TOKEN` with your Apify API token
   - Replace `YOUR_TELEGRAM_BOT_NAME` with your Telegram bot name

## Database Schema

The NocoDB table requires the following columns:

- `url` (string): Link to the original listing
- `title` (string): Title of the listing
- `location` (string): Location/neighborhood
- `price` (number): Monthly rent
- `rooms` (string/number): Number of rooms
- `area` (number): Size in square meters
- `source` (string): Where the listing was found (Gewobag, eBay)
- `date_scraped` (date): When the listing was collected
- `status` (string): Availability status
- `description` (string): Full listing description
- `images` (string): JSON string of image URLs
- `date_posted` (date): When the listing was originally posted

## Usage

Once deployed, users can:

1. Message the Telegram bot with their housing preferences
2. Receive matching listings based on their criteria
3. Request to apply for a specific listing
4. Provide a brief self-description
5. Receive an AI-generated application letter customized to both the listing and their profile

Example user flow:
```
User: "I'm looking for a 2-room apartment in Kreuzberg under 1000€"
Bot: [Shows matching listings]
User: "I'd like to apply for the first one"
Bot: "Great! Please tell me a bit about yourself"
User: "I'm a software engineer working at a startup. I'm quiet, non-smoker, and looking for a long-term rental."
Bot: [Generates personalized application letter]
```

## Customization

You can customize:

- Scraping schedule by adjusting the Schedule Trigger nodes
- AI prompts in the "Data analyst" and "Writer" nodes
- Filtering logic in the NocoDB query formulation
- Application letter style and format

## Troubleshooting

- Check that all API credentials are valid
- Verify your NocoDB schema matches the expected format
- Ensure the Apify actors are properly configured
- Check n8n execution logs for any errors
