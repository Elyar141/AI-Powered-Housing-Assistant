# Setup Guide for AI-Powered Housing Assistant

This document provides detailed instructions for setting up the AI-Powered Housing Assistant workflow in n8n.

## Step 1: Prerequisites

Before beginning, ensure you have:

- A running n8n instance (self-hosted or cloud)
- Accounts with the following services:
  - [NocoDB](https://nocodb.com/) - For database storage
  - [Telegram](https://telegram.org/) - For the bot interface
  - [Apify](https://apify.com/) - For web scraping
  - [OpenAI](https://openai.com/) - For AI capabilities

## Step 2: Database Setup

### Create NocoDB Database

1. Login to your NocoDB account
2. Create a new project for housing listings
3. Create a table with the following columns:

| Column Name   | Type         | Description                             |
|---------------|-------------|-----------------------------------------|
| url           | String      | URL of the housing listing              |
| title         | String      | Title of the listing                    |
| location      | String      | Neighborhood or area                    |
| price         | Number      | Monthly rent                            |
| rooms         | String      | Number of rooms                         |
| area          | Number      | Size in square meters                   |
| wbs_required  | Boolean     | If housing voucher is needed            |
| source        | String      | Source of listing (Gewobag, eBay)       |
| date_scraped  | Date        | When the listing was scraped            |
| status        | String      | Availability status                     |
| description   | Text        | Full description of the listing         |
| images        | Text        | JSON string containing image URLs       |
| date_posted   | Date        | When the listing was originally posted  |

4. Note your Workspace ID, Project ID, and Table ID from the URL when viewing your table

## Step 3: Telegram Bot Setup

1. Open Telegram and search for "BotFather"
2. Send the command `/newbot` to create a new bot
3. Follow the prompts to name your bot
4. Once created, BotFather will provide a token - save this for later
5. Customize your bot with `/setdescription` and `/setuserpic` commands

## Step 4: Apify Setup

### For Gewobag Scraper:
1. Create a new task in Apify
2. Select "Web Scraper" as the actor
3. Configure it to scrape Gewobag's listing pages
4. Save the actor task ID

### For eBay Scraper:
1. Create another task in Apify
2. Select "Web Scraper" as the actor
3. Configure it to scrape eBay Kleinanzeigen's housing listings
4. Save the actor task ID

## Step 5: OpenAI API Setup

1. Create an account on OpenAI (if you don't have one)
2. Navigate to API keys section
3. Generate a new API key
4. Save the API key for use in n8n

## Step 6: Import Workflow to n8n

1. Open your n8n instance
2. Go to Workflows
3. Click "Import from File"
4. Select the cleaned workflow JSON file
5. Click "Import"

## Step 7: Configure Credentials in n8n

### NocoDB Credentials
1. In n8n, go to Settings > Credentials
2. Add new credential of type "NocoDB API Token"
3. Enter your NocoDB API token
4. Save the credential

### Telegram Credentials
1. Add new credential of type "Telegram API"
2. Enter the bot token you received from BotFather
3. Save the credential

### OpenAI Credentials
1. Add new credential of type "OpenAI API"
2. Enter your OpenAI API key
3. Save the credential

## Step 8: Configure the Workflow

Replace all placeholder values in the workflow with your actual values:

1. `YOUR_WORKSPACE_ID` → Your NocoDB workspace ID
2. `YOUR_PROJECT_ID` → Your NocoDB project ID
3. `YOUR_TABLE_ID` → Your NocoDB table ID
4. `YOUR_ACTOR_TASK_ID` → Your Apify actor task IDs
5. `YOUR_APIFY_TOKEN` → Your Apify API token
6. `WEBHOOK_ID_PLACEHOLDER` → Will be auto-generated when activated
7. `CREDENTIALS_ID_PLACEHOLDER` → Select appropriate credentials from dropdowns

## Step 9: Activate and Test

1. Click "Save" to save the workflow
2. Activate the workflow using the toggle at the top
3. Test each component:
   - Manual execute the Gewobag scraper
   - Manual execute the eBay scraper
   - Send a message to your Telegram bot

## Step 10: Customize (Optional)

Feel free to customize:

- Scraping schedules (by adjusting the Schedule Trigger nodes)
- AI prompts (in the "Data analyst" and "Writer" nodes)
- Filtering logic
- Application letter format and style

## Troubleshooting

If you encounter issues:

- Check execution logs in n8n
- Verify all credentials are correct
- Ensure NocoDB table structure matches expected schema
- Confirm Apify tasks are properly configured and running
- Test OpenAI API access independently