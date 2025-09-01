# 🔐 CRITICAL SECURITY SETUP REQUIRED

## ⚠️ IMPORTANT: Complete These Steps Before Using the Workflows

The workflows have been updated to remove hardcoded API keys and secure webhook endpoints. You MUST complete the following setup steps:

## 1. API Credentials Setup

### Create n8n Credentials for Each API Service:

#### Google API Credential
1. Go to n8n → Credentials → Add Credential
2. Choose "Generic Credential Type" 
3. Name: `YOUR_GOOGLE_API_CREDENTIAL`
4. Add field: `api_key` = `YOUR_GOOGLE_CUSTOM_SEARCH_API_KEY`

#### Google Search Engine ID
1. Create another credential: `YOUR_GOOGLE_SEARCH_ENGINE_ID`  
2. Add field: `cx` = `YOUR_CUSTOM_SEARCH_ENGINE_ID`

#### Firecrawl API Credential
1. Create credential: `YOUR_FIRECRAWL_API_CREDENTIAL`
2. Add field: `api_key` = `YOUR_FIRECRAWL_API_KEY`

#### Pexels API Credential  
1. Create credential: `YOUR_PEXELS_API_CREDENTIAL`
2. Add field: `api_key` = `YOUR_PEXELS_API_KEY`

## 2. Webhook Security Setup

All webhook endpoints now require authentication headers. When calling webhooks, include:

```bash
# Example webhook call with authentication
curl -X POST https://your-n8n-instance.com/webhook/ar-blog-fetch-articles \
  -H "Authorization: Bearer YOUR_WEBHOOK_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"your": "data"}'
```

### Configure Webhook Authentication:
1. In n8n, go to each workflow's webhook node
2. Under "Authentication" → "Header Auth"
3. Set Header Name: `Authorization`
4. Set Header Value: `Bearer YOUR_SECRET_TOKEN`

## 3. Generate Secure Tokens

For webhook authentication, generate secure random tokens:

```bash
# Generate secure tokens (use different tokens for each webhook)
openssl rand -base64 32
```

## 4. Updated Webhook Endpoints

- `ar-blog-fetch-articles` → Now requires POST + Authorization header
- `get-queries` → Now requires POST + Authorization header  
- `ma3l0mah-get-generate-blog` → Now requires POST + Authorization header

## 5. Environment Variables (Recommended)

Instead of storing credentials in n8n, use environment variables:

```bash
export GOOGLE_API_KEY="your_api_key_here"
export FIRECRAWL_API_KEY="your_api_key_here" 
export PEXELS_API_KEY="your_api_key_here"
export WEBHOOK_AUTH_TOKEN="your_secure_token_here"
```

## ⚠️ CRITICAL VULNERABILITIES FIXED

✅ **Removed hardcoded API keys** - Replaced with credential references
✅ **Added webhook authentication** - All endpoints now require authorization
✅ **Secured HTTP methods** - Changed to POST-only for better security

## 🔄 Next Steps

1. Replace all credential references with your actual API keys
2. Test workflows with new authentication setup
3. Monitor for unauthorized access attempts
4. Regularly rotate API keys and webhook tokens
5. Consider implementing rate limiting at the infrastructure level

---

**⚠️ WARNING**: Do not commit actual API keys to version control. Keep this file for reference only.