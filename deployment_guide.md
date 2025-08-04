# Deployment Guide

This guide covers various deployment options for the dataPARC Chatbot Widget, from simple testing to production environments.

## 🚀 Quick Deployment Options

### 1. GitHub Pages (Recommended for Demo)

**Setup Time**: 5 minutes | **Cost**: Free | **Difficulty**: Easy

```bash
# 1. Create new GitHub repository
# 2. Upload index.html as main file
# 3. Go to repository Settings > Pages
# 4. Select "Deploy from a branch" > main
# 5. Your chatbot will be available at:
https://yourusername.github.io/repository-name
```

**Pros**: Free, automatic SSL, version control, easy sharing
**Cons**: Public repository required for free tier

### 2. Netlify Drop Deploy

**Setup Time**: 2 minutes | **Cost**: Free | **Difficulty**: Very Easy

```bash
# 1. Go to netlify.com
# 2. Drag and drop your index.html file
# 3. Get instant URL like: https://amazing-name-123456.netlify.app
# 4. Optional: Connect custom domain
```

**Pros**: Instant deployment, custom domains, CDN, HTTPS
**Cons**: Random URL unless you upgrade

### 3. Vercel

**Setup Time**: 3 minutes | **Cost**: Free | **Difficulty**: Easy

```bash
# 1. Install Vercel CLI: npm i -g vercel
# 2. In project folder: vercel
# 3. Follow prompts
# 4. Get production URL
```

**Pros**: Excellent performance, automatic deployments, custom domains
**Cons**: Requires Node.js/npm installed

## 🏢 Production Deployment

### Option 1: AWS S3 + CloudFront

**Best for**: Enterprise, high traffic, global audience

#### Step-by-Step AWS Deployment

```bash
# 1. Create S3 Bucket
aws s3 mb s3://dataparc-chatbot-demo

# 2. Upload files
aws s3 cp index.html s3://dataparc-chatbot-demo/ --acl public-read

# 3. Enable static website hosting
aws s3 website s3://dataparc-chatbot-demo --index-document index.html

# 4. Create CloudFront distribution (optional but recommended)
```

**Monthly Cost**: $1-5 for typical usage
**Features**: Global CDN, SSL certificates, custom domains

#### CloudFront Configuration
```json
{
  "Origins": [{
    "DomainName": "dataparc-chatbot-demo.s3.amazonaws.com",
    "OriginPath": "",
    "CustomOriginConfig": {
      "HTTPPort": 80,
      "HTTPSPort": 443,
      "OriginProtocolPolicy": "http-only"
    }
  }],
  "DefaultCacheBehavior": {
    "TargetOriginId": "S3-dataparc-chatbot-demo",
    "ViewerProtocolPolicy": "redirect-to-https"
  }
}
```

### Option 2: Traditional Web Server

**Best for**: Existing infrastructure, on-premise hosting

#### Apache Configuration
```apache
# .htaccess file
<IfModule mod_mime.c>
    AddType text/html .html
    AddType application/javascript .js
    AddType text/css .css
</IfModule>

# Enable compression
<IfModule mod_deflate.c>
    AddOutputFilterByType DEFLATE text/html text/css application/javascript
</IfModule>

# Browser caching
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresByType text/html "access plus 1 hour"
    ExpiresByType text/css "access plus 1 month"
    ExpiresByType application/javascript "access plus 1 month"
</IfModule>
```

#### Nginx Configuration
```nginx
server {
    listen 80;
    server_name demo.dataparc.com;
    
    # Redirect to HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl;
    server_name demo.dataparc.com;
    
    ssl_certificate /path/to/certificate.crt;
    ssl_certificate_key /path/to/private.key;
    
    root /var/www/chatbot;
    index index.html;
    
    # Gzip compression
    gzip on;
    gzip_types text/html text/css application/javascript;
    
    # Browser caching
    location ~* \.(css|js)$ {
        expires 1M;
        add_header Cache-Control "public, immutable";
    }
    
    location / {
        try_files $uri $uri/ =404;
    }
}
```

## 🔗 Integration with Existing dataPARC Website

### Method 1: Direct Integration

```html
<!-- Add to existing dataPARC pages -->
<!-- Before closing </body> tag -->

<!-- Option A: Inline integration -->
<script>
// Copy the entire chatbot JavaScript class here
// This method includes everything in your existing pages
</script>

<!-- Option B: External file -->
<script src="/assets/js/dataparc-chatbot.js"></script>
<link rel="stylesheet" href="/assets/css/dataparc-chatbot.css">
```

### Method 2: Content Management System

#### WordPress Integration
```php
// functions.php
function add_dataparc_chatbot() {
    if (!is_admin()) {
        wp_enqueue_script(
            'dataparc-chatbot', 
            get_template_directory_uri() . '/js/chatbot.js', 
            array(), 
            '1.2.0', 
            true
        );
        wp_enqueue_style(
            'dataparc-chatbot-css', 
            get_template_directory_uri() . '/css/chatbot.css', 
            array(), 
            '1.2.0'
        );
    }
}
add_action('wp_enqueue_scripts', 'add_dataparc_chatbot');

// Add to footer
function add_chatbot_html() {
    echo '<div id="dataparc-chatbot-container"></div>';
}
add_action('wp_footer', 'add_chatbot_html');
```

#### Drupal Integration
```php
// In your theme's .libraries.yml
chatbot:
  js:
    js/dataparc-chatbot.js: {}
  css:
    theme:
      css/dataparc-chatbot.css: {}

// In your theme or module
function mymodule_page_attachments(array &$attachments) {
  $attachments['#attached']['library'][] = 'mytheme/chatbot';
}
```

## 📊 Performance Optimization

### Content Delivery Network (CDN)

```html
<!-- Host static assets on CDN -->
<link rel="preload" href="https://cdn.dataparc.com/chatbot/v1.2/styles.css" as="style">
<link rel="preload" href="https://cdn.dataparc.com/chatbot/v1.2/script.js" as="script">

<link rel="stylesheet" href="https://cdn.dataparc.com/chatbot/v1.2/styles.css">
<script src="https://cdn.dataparc.com/chatbot/v1.2/script.js" defer></script>
```

### Minification and Compression

```bash
# Using online tools or build process
# HTML: Remove whitespace, comments
# CSS: Minify, remove unused styles
# JS: Minify, optimize

# Example with basic tools:
npx html-minifier --collapse-whitespace --remove-comments index.html > index.min.html
```

### Lazy Loading
```javascript
// Load chatbot only when needed
function loadChatbot() {
    if (!window.dataPARCChatbotLoaded) {
        // Initialize chatbot
        window.dataPARCChatbot = new DataPARCChatbot();
        window.dataPARCChatbotLoaded = true;
    }
}

// Load on first interaction
document.addEventListener('scroll', loadChatbot, { once: true });
document.addEventListener('click', loadChatbot, { once: true });
```

## 🔒 Security Considerations

### HTTPS Configuration
```nginx
# Force HTTPS
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;

# Content Security Policy
add_header Content-Security-Policy "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline';" always;

# Additional security headers
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
```

### Data Privacy
```javascript
// Implement data retention policies
class ChatbotAnalytics {
    constructor() {
        this.maxLogAge = 30 * 24 * 60 * 60 * 1000; // 30 days
        this.cleanupInterval = setInterval(() => {
            this.cleanupOldLogs();
        }, 24 * 60 * 60 * 1000); // Daily cleanup
    }
    
    cleanupOldLogs() {
        const cutoff = Date.now() - this.maxLogAge;
        this.conversationLog = this.conversationLog.filter(
            log => new Date(log.timestamp).getTime() > cutoff
        );
    }
}
```

## 🌐 Custom Domain Setup

### Subdomain Configuration
```dns
# DNS Records for demo.dataparc.com
CNAME demo.dataparc.com yourusername.github.io
# OR
A demo.dataparc.com 192.30.252.153
A demo.dataparc.com 192.30.252.154
```

### SSL Certificate Setup
```bash
# Using Let's Encrypt with Certbot
sudo certbot --nginx -d demo.dataparc.com

# Or using AWS Certificate Manager (ACM) with CloudFront
aws acm request-certificate --domain-name demo.dataparc.com
```

## 📱 Mobile App Integration

### WebView Integration (iOS/Android)
```javascript
// Detect mobile app environment
function isMobileApp() {
    return window.ReactNativeWebView || 
           window.webkit?.messageHandlers || 
           window.Android;
}

// Mobile app specific configurations
if (isMobileApp()) {
    // Adjust styling for mobile app
    document.body.classList.add('mobile-app');
    
    // Disable certain features
    document.querySelector('.chatbot-toggle').style.bottom = '100px';
}
```

## 🔄 Continuous Deployment

### GitHub Actions Workflow
```yaml
# .github/workflows/deploy.yml
name: Deploy Chatbot

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./
```

## 📈 Monitoring and Analytics

### Production Monitoring
```javascript
// Error tracking
window.addEventListener('error', (event) => {
    // Send to monitoring service
    fetch('/api/errors', {
        method: 'POST',
        body: JSON.stringify({
            message: event.message,
            filename: event.filename,
            lineno: event.lineno,
            timestamp: new Date().toISOString()
        })
    });
});

// Performance monitoring
const observer = new PerformanceObserver((list) => {
    for (const entry of list.getEntries()) {
        if (entry.entryType === 'measure') {
            // Track custom metrics
            console.log(`${entry.name}: ${entry.duration}ms`);
        }
    }
});
observer.observe({entryTypes: ['measure']});
```

---

## Support

For deployment issues or questions:
- 📧 Email: deployment-support@dataparc.com  
- 📖 Documentation: [GitHub Wiki](https://github.com/yourusername/dataparc-chatbot/wiki)
- 🐛 Issues: [GitHub Issues](https://github.com/yourusername/dataparc-chatbot/issues)