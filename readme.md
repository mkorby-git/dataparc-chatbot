# dataPARC Chatbot Widget

A lightweight, responsive chatbot widget designed for the main dataPARC website, or dataPARC Community Forum, to help visitors find Sales, Support, and Documentation resources quickly and efficiently.

![Chatbot Demo](assets/chatbot-preview.png)

## 🚀 Features

- **Intent Recognition** - Automatically detects user needs (Sales, Support, Documentation, Demo requests)
- **Mobile Optimized** - Responsive design works on all devices, specially optimized for iPhone 15+ and large phones
- **Quick Actions** - Pre-defined buttons for common user requests
- **Analytics Tracking** - Built-in conversation logging and interaction analytics
- **Easy Integration** - Single HTML file, no external dependencies
- **Professional Design** - Matches dataPARC branding and industrial aesthetic
- **Lightweight** - ~15KB total bundle size

## 📱 Device Support

| Device Type | Screen Size | Status |
|-------------|-------------|--------|
| iPhone 15+ | 430px+ | ✅ Optimized |
| Large Phones | 481-768px | ✅ Optimized |
| Small Phones | <480px | ✅ Supported |
| Tablets | 769-1024px | ✅ Supported |
| Desktop | 1025px+ | ✅ Supported |

## 🎯 Use Cases

### Primary Functions
- **Sales Inquiries** - Route users to sales team, pricing, and demo requests
- **Technical Support** - Connect users with support resources and ticket system
- **Documentation** - Guide users to relevant guides, APIs, and training materials
- **Demo Requests** - Facilitate product demonstration scheduling

### Intent Keywords
- **Sales**: pricing, cost, buy, purchase, quote, demo
- **Support**: help, technical, issue, problem, troubleshoot
- **Documentation**: docs, manual, guide, tutorial, instructions
- **Demo**: demonstration, show me, trial, test

## 🛠️ Quick Start

### Option 1: Direct Use
1. Download `index.html`
2. Open in any modern web browser
3. Test the chatbot functionality

### Option 2: Web Server Deployment
1. Upload `index.html` to your web server
2. Access via your domain: `https://yourdomain.com/chatbot-demo`
3. Share the URL with stakeholders

### Option 3: GitHub Pages
1. Fork this repository
2. Enable GitHub Pages in repository settings
3. Access via: `https://yourusername.github.io/dataparc-chatbot`

## 📊 Analytics

The chatbot includes built-in analytics tracking:

```javascript
// Access analytics data in browser console
getChatbotAnalytics()

// Returns:
{
  conversationLog: [...],
  totalInteractions: 15,
  chatOpenedCount: 3,
  messagesCount: 8,
  intentMatches: [...]
}
```

### Tracked Events
- Widget loaded
- Chat opened/closed
- Messages sent
- Intent matches
- Quick actions clicked
- Fallback responses

## 🎨 Customization

### Theme Colors
```css
/* Primary brand color */
--primary-color: #3b82f6;
--primary-dark: #1e3a8a;

/* Update in CSS for custom branding */
.chatbot-header {
  background: linear-gradient(135deg, var(--primary-color), var(--primary-dark));
}
```

### Response Customization
```javascript
// Update responses in the DataPARCChatbot class
this.responses = {
  sales: {
    keywords: ['sales', 'pricing', 'cost'],
    response: "Your custom sales message",
    actions: [...]
  }
}
```

## 🔧 Technical Architecture

### Technology Stack
- **Frontend**: Pure HTML5, CSS3, Vanilla JavaScript (ES6+)
- **Styling**: CSS Grid, Flexbox, Custom Properties
- **Storage**: In-memory JavaScript objects
- **Analytics**: Browser console logging
- **Dependencies**: None (completely self-contained)

### Browser Compatibility
- ✅ Chrome 80+
- ✅ Firefox 75+
- ✅ Safari 13+
- ✅ Edge 80+
- ✅ Mobile browsers (iOS Safari, Chrome Android)

### Performance
- **Bundle Size**: ~15KB (HTML + CSS + JS)
- **Load Time**: <100ms (no external requests)
- **Memory Usage**: <2MB
- **First Paint**: <50ms

## 📁 Project Structure

```
dataparc-chatbot/
├── index.html               # Main demo file
├── README.md                # This documentation
├── CHANGELOG.md             # Version history
├── LICENSE                  # MIT License
├── assets/
│   ├── screenshots/        # Demo images
│   └── docs/               # Additional documentation
├── versions/
│   ├── v1.0-basic.html     # Version archive
│   ├── v1.1-mobile.html    # Mobile optimizations
│   └── v1.2-current.html   # Latest version
└── examples/
    ├── embed-example.html  # Integration example
    └── custom-theme.html   # Theming example
```

## 🚀 Deployment Options

### Production Deployment

1. **Static Hosting**
   - AWS S3 + CloudFront
   - Azure Blob Storage
   - Google Cloud Storage
   - Netlify/Vercel

2. **Traditional Web Server**
   - Apache/Nginx
   - IIS
   - Node.js/Express

3. **CDN Integration**
   ```html
   <script src="https://cdn.dataparc.com/chatbot/v1.2/widget.js"></script>
   ```

### Integration Methods

#### Embed in Existing Site
```html
<!-- Add before closing </body> tag -->
<div id="dataparc-chatbot"></div>
<script src="chatbot-widget.js"></script>
<script>
  DataPARCChatbot.init({
    container: '#dataparc-chatbot',
    theme: 'dataparc-blue'
  });
</script>
```

#### WordPress Plugin
```php
function add_dataparc_chatbot() {
    wp_enqueue_script('dataparc-chatbot', 'path/to/widget.js');
}
add_action('wp_enqueue_scripts', 'add_dataparc_chatbot');
```

## 📈 Roadmap

### Version 1.3 (Planned)
- [ ] Backend API integration
- [ ] CRM lead capture (Salesforce/HubSpot)
- [ ] Advanced analytics dashboard
- [ ] A/B testing framework
- [ ] Multi-language support

### Version 2.0 (Future)
- [ ] AI-powered responses
- [ ] Voice interaction
- [ ] Video chat integration
- [ ] Advanced conversation flows
- [ ] Admin management panel

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Setup
```bash
# Clone the repository
git clone https://github.com/yourusername/dataparc-chatbot.git

# Navigate to project
cd dataparc-chatbot

# Open in browser (no build process required)
open index.html
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/dataparc-chatbot/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/dataparc-chatbot/discussions)
- **Email**: chatbot-support@dataparc.com

## 🏆 Acknowledgments

- Built for the dataPARC IDI (Industrial Data Intelligence) platform
- Optimized for industrial website user experience
- Designed with mobile-first responsive principles

---

**Made with ❤️ for dataPARC**
