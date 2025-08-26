# Ma3l0mah AI Arabic Blogger - Complete n8n Workflow System

## 🎯 Project Overview

**Ma3l0mah AI Arabic Blogger** is a complete automated content creation and publishing system built with n8n workflows. This project transforms English scientific articles into engaging Arabic content for the Middle Eastern audience, featuring automated research query generation, article fetching, AI-powered translation and adaptation, and multi-channel publishing.

## 🧩 Workflow Components

### 1. **blogger-ar-queries-agent.json** - AI Query Generator
**Purpose**: Generates trending and evergreen search queries for Arabic audiences interested in psychology, neuroscience, and science topics.

**Key Features**:
- Uses AI agents with Perplexity Deep Search and Google Gemini
- Produces 20 culturally relevant search queries (70% evergreen, 30% trending)
- Stores queries in Airtable for systematic processing
- Focuses on MENA region interests and search patterns

### 2. **blogger-ar-fetch-articles.json** - Multi-Source Article Fetcher
**Purpose**: Searches and collects articles from multiple scientific publications based on generated queries.

**Key Features**:
- Searches 5 major science publications simultaneously:
  - Psychology Today
  - Scientific American
  - Live Science
  - Big Think
  - Greater Good Berkeley
- Uses Google Custom Search API with targeted filters
- Extracts metadata, images, and article previews
- Stores results in Airtable with deduplication

### 3. **ma3l0mah-get-generate-blog.json** - Complete Content Pipeline
**Purpose**: The main workflow that transforms source articles into published Arabic blog posts and social media content.

**Complete Process Flow**:
1. **Content Scraping**: Uses Firecrawl to extract full article content
2. **Image Generation**: Fetches relevant images from Pexels API
3. **SEO Optimization**: Generates Arabic SEO titles, slugs, and meta descriptions
4. **Content Transformation**: Creates comprehensive Arabic blog posts with cultural adaptation
5. **Multi-Channel Publishing**: 
   - Posts to Blogger platform
   - Sends Telegram messages to Arabic channels
   - Email notifications for review
6. **Data Management**: Updates Airtable records with publication status

## 🚀 Quick Start Guide

### Prerequisites
Before setting up these workflows, ensure you have:

- n8n instance (cloud or self-hosted)
- Google Custom Search API key and search engine ID
- Airtable account and API access
- Firecrawl API key
- Pexels API key
- Google OAuth2 credentials for Blogger
- Telegram Bot token
- Anthropic/OpenAI API keys

### Step 1: Import Workflows

Copy and paste each JSON file into your n8n instance:

1. Go to n8n → Workflows → Import from file
2. Paste the JSON content for each workflow
3. Save and activate each workflow

### Step 2: Configure API Credentials

Set up the following credentials in your n8n instance:

**Google APIs**:
```
Credential Type: Google OAuth2 API
Use for: Custom Search, Blogger API
Scopes: https://www.googleapis.com/auth/blogger
```

**Airtable Integration**:
```
Credential Type: Airtable OAuth2 API
Base ID: [Your Airtable Base ID]
```

**AI Services**:
```
Anthropic API: [Your Anthropic API Key]
Google Gemini API: [Your Google AI Studio API Key]
Perplexity API: [Your Perplexity API Key]
```

**Content Services**:
```
Firecrawl API: [Your Firecrawl API Key]
Pexels API: [Your Pexels API Key]
```

**Communication**:
```
Telegram Bot API: [Your Bot Token]
Gmail OAuth2: [Your Gmail credentials]
```

### Step 3: Set Up Airtable Database

Create an Airtable base with these tables:

**Queries Table**:
- `query` (Single line text)
- `freshness` (Select: daily, weekly)
- `status` (Select: new, fetched, failed)
- `last_run_at` (Date & time)
- `error_log` (Long text)

**Articles Table**:
- `url` (URL)
- `search_query` (Single line text)
- `site` (Single line text)
- `title` (Single line text)
- `description` (Long text)
- `author` (Single line text)
- `published_at` (Date & time)
- `image_url` (URL)
- `article_html` (Long text)
- `word_count` (Number)
- `status` (Select: new, posted, failed, enriched)
- `blog_post_url` (URL)
- `blog_post_id` (Single line text)
- `error_log` (Long text)

**Blogs Table**:
- `blog_id` (Single line text)
- `url` (URL)
- `title` (Single line text)
- `blog_html` (Long text)
- `Status` (Single line text)

### Webhook URLs for Manual Testing

After importing the workflows, use these webhook paths for testing:

- **Query Generator**: `<your-webhook-url>`
- **Article Fetcher**: `<your-webhook-url>`
- **Content Pipeline**: `<your-webhook-url>`


## 🛠 Advanced Configuration

### Custom AI Prompts

The system uses several AI prompts that can be customized:

**Query Generation Prompt** (in blogger-ar-queries-agent.json):
- Modify the system message to focus on different topics
- Adjust the demographic targeting
- Change the evergreen/trending ratio

**Content Creation Prompt** (in ma3l0mah-get-generate-blog.json):
- Customize the Arabic writing style
- Modify the SEO guidelines
- Adjust the content structure and sections

**Social Media Prompt** (in ma3l0mah-get-generate-blog.json):
- Change the Telegram post format
- Modify the hashtag strategy
- Adjust the tone and voice

### Adding New Content Sources

To add new scientific publications to the article fetcher:

1. Duplicate an existing HTTP Request node in blogger-ar-fetch-articles.json
2. Modify the search query parameters for the new site
3. Add a new Code node to process the results
4. Connect it to the main Upsert Articles Records node

### Multi-Language Support

The system can be adapted for other languages by:

1. Modifying the AI prompts in the content generation workflow
2. Updating the search queries to target different language publications
3. Adjusting the Airtable field names and structure as needed

## 📊 Monitoring & Analytics

### Workflow Execution Tracking

Monitor your workflows through:

- n8n execution history for success/failure rates
- Airtable records for content pipeline status
- Telegram channel analytics for engagement metrics
- Google Search Console for blog SEO performance

### Key Metrics to Track

- **Query Generation**: Number of queries generated per run
- **Article Fetching**: Success rate of article discovery
- **Content Creation**: Time from source to published article
- **Engagement**: Social media shares and blog traffic

## 🔧 Troubleshooting

### Common Issues and Solutions

**API Rate Limits**:
- Add wait nodes between API calls
- Implement retry logic with exponential backoff
- Use multiple API keys for high-volume usage

**Content Quality Issues**:
- Refine AI prompts for better output
- Add content validation nodes
- Implement human review checkpoints

**Database Sync Problems**:
- Check Airtable API limits
- Verify field mapping in Upsert operations
- Monitor for duplicate records

### Error Handling

The workflows include built-in error handling:
- Failed executions are logged in Airtable
- Email notifications for critical failures
- Automatic retry mechanisms for temporary issues

## 🤝 Contributing

To improve or extend this system:

1. Fork the workflow configurations
2. Test changes in a development environment
3. Document any new features or modifications
4. Share improvements with the community

## 📄 License

This project is open source and available under the MIT License. Feel free to use, modify, and distribute as needed.

## 🆘 Support

For setup assistance or troubleshooting:

1. Check the n8n community forums
2. Review the API documentation for each service
3. Test individual workflow nodes for debugging
4. Monitor the execution logs for specific error messages

---

**Note**: This system is designed for educational and legitimate content creation purposes. Ensure you comply with all API terms of service and content licensing requirements when using this system.