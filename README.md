<div align="center">

# 🚀 WebEmbed Advanced

### The Ultimate Discord Embed Generator

*Create beautiful, feature-rich Discord embeds with custom URLs, analytics, and infinite possibilities*

[![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)](https://github.com/yourusername/webembed)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Node](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)](https://nodejs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.3-blue.svg)](https://www.typescriptlang.org/)

[Features](#-features) • [Quick Start](#-quick-start) • [API Docs](#-api-reference) • [Examples](#-usage-examples) • [Selfbot Guide](#-discord-selfbot-integration)

---

</div>

## 🎯 Why WebEmbed Advanced?

Transform ordinary links into **stunning Discord embeds** with full customization, analytics tracking, and powerful features that go way beyond basic embed generators.

```javascript
// Send this URL in Discord:
https://your-server.com/e/gaming-night

// Discord shows this beautiful embed:
┌──────────────────────────────────┐
│  🎮 Gaming Night!                │
│  Join us for epic gaming         │
│  sessions tonight!               │
│                                  │
│  Time: 8 PM EST                  │
│  Game: Valorant                  │
│  [Cool gaming image]             │
└──────────────────────────────────┘
```

## ✨ Features That Make Us Stand Out

<table>
<tr>
<td width="50%">

### 🎨 Rich Discord Embeds
- Full embed customization (25 fields!)
- Custom colors, images, videos
- Footers, timestamps, authors
- Multiple fields with inline support
- Thumbnail & full-size images

</td>
<td width="50%">

### 🔗 Smart URL Management
- Custom aliases (`/e/cool-link`)
- Auto-generated short IDs
- Clean, shareable URLs
- oEmbed protocol support
- URL redirect capability

</td>
</tr>
<tr>
<td width="50%">

### 📊 Advanced Analytics
- Real-time view tracking
- Unique visitor counting
- 24-hour activity stats
- IP-based analytics
- Referrer tracking

</td>
<td width="50%">

### 🔐 Enterprise Security
- API key authentication
- Multi-tier rate limiting
- CORS protection
- Helmet.js security headers
- SQL injection prevention

</td>
</tr>
<tr>
<td width="50%">

### ⏰ Smart Features
- Auto-expiring embeds
- Scheduled cleanup
- Persistent SQLite storage
- Background auto-save
- Graceful shutdown handling

</td>
<td width="50%">

### 🛠️ Developer Friendly
- Full TypeScript support
- Comprehensive API docs
- Code examples (JS, Python, cURL)
- Docker ready
- Hot reload in dev mode

</td>
</tr>
</table>

## 🚀 Quick Start

Get up and running in **60 seconds**!

### Prerequisites

```bash
Node.js >= 18.0.0 (v20 LTS recommended)
npm or yarn
```

### Windows Users - Easy Setup! 🪟

```powershell
# 1. Run the automated setup script
.\setup.ps1

# That's it! Server starts automatically 🎉
```

### Manual Installation (All Platforms)

```bash
# 1️⃣ Clone the repository
git clone <your-repo-url>
cd WebEmbed

# 2️⃣ Install dependencies  
npm install

# 3️⃣ Configure environment (optional - works with defaults)
cp .env.example .env

# 4️⃣ Start development server
npm run dev

# 🎉 Server running at http://localhost:3000
```

### Verify Installation

```bash
# Test the API
.\test.ps1

# Or visit in browser
http://localhost:3000
```

### Production Build
Reference

### Core Endpoints

<details>
<summary><b>POST /api/embeds</b> - Create a new embed</summary>

#### Request Body
```javascript
{
  // Basic Info
  "title": "Your Title",           // Max 256 chars
  "description": "Description",    // Max 4096 chars
  "url": "https://link.com",       // Clickable title URL
  "color": "#5865F2",              // Hex color
  
  // Media
  "imageUrl": "https://...",       // Large image
  "thumbnailUrl": "https://...",   // Small thumbnail
  "videoUrl": "https://...",       // Video embed
  
  // Author
  "authorName": "John Doe",
  "authorUrl": "https://...",
  "authorIconUrl": "https://...",
  
  // Footer
  "footerText": "Footer text",
  "footerIconUrl": "https://...",
  
  // Fields (max 25)
  "fields": [
    {
      "name": "Field Name",
      "value": "Field Value",
      "inline": true             // Optional
    }
  ],
  
  // Advanced
  "alias": "custom-url",         // Custom short URL
  "timestamp": "2026-02-18T12:00:00Z",
  "redirectUrl": "https://...",  // Auto-redirect
  "expiresIn": 3600,            // Seconds until expiry
  
  // Provider (for oEmbed)
  "providerName": "Site Name",
  "providerUrl": "https://..."
}
```

#### Response
```json
{
  "success": true,
  "embed": {
    "id": "abc123xyz",
    "alias": "custom-url",
    "url": "http://localhost:3000/e/custom-url",
    "shortUrl": "http://localhost:3000/e/custom-url",
    "oembedUrl": "http://localhost:3000/oembed/abc123xyz",
    "createdAt": 1708257600000,
    "expiresAt": 1708261200000
  }
}
```

#### Example - cURL
```bash
curl -X POST http://localhost:3000/api/embeds \
  -H "Content-Type: application/json" \
  -d '{
    "title": "🎮 Gaming Night",
    "description": "Join us tonight!",
    "color": "#FF6B6B",
    "alias": "gaming",
    "fields": [
      {"name": "Time", "value": "8 PM EST", "inline": true},
      {"name": "Game", "value": "Valorant", "inline": true}
    ]
  }'
```

#### Example - JavaScript
```javascript
const response = await fetch('http://localhost:3000/api/embeds', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    title: '✨ My Embed',
    description: 'Check this out!',
    color: '#00FF00'
  })
});

const { embed } = await response.json();
console.log('Share this:', embed.url);
```

#### Example - Python
```python
import requests

response = requests.post('http://localhost:3000/api/embeds', json={
    'title': 'Python Embed',
    'description': 'Made with Python!',
    'color': '#3776AB'
})

embed = response.json()['embed']
print(f"URL: {embed['url']}")
```

</details>

<details>
<summary><b>GET /e/:idOrAlias</b> - View embed (Discord preview)</summary>

#### Usage
```
http://localhost:3000/e/abc123      # By ID
http://localhost:3000/e/gaming      # By alias
```

#### Response
Returns HTML page with Discord embed meta tags. When shared in Discord, shows the embed preview.

#### Features
- Auto-increments view counter
- Logs analytics (IP, user agent, referer)
- Handles expired embeds (410 Gone)
- Handles disabled embeds (403 Forbidden)
- Auto-redirects if `redirectUrl` is set

</details>

<details>
<summary><b>GET /api/embeds/:id/stats</b> - Get analytics <i>(requires API key)</i></summary>

#### Request
```bash
curl http://localhost:3000/api/embeds/abc123/stats \
  -H "X-API-Key: your-api-key"
```

#### Response
```json
{
  "totalViews": 1547,
  "uniqueIps": 892,
  "last24Hours": 156,
  "createdAt": 1708257600000
}
```

</details>
💡 Usage Examples

### Example 1: Simple Announcement
```javascript
const embed = {
  title: "📢 Server Announcement",
  description: "We're hosting a giveaway!",
  color: "#FFD700",
  fields: [
    { name: "Prize", value: "Nitro", inline: true },
    { name: "Duration", value: "48 hours", inline: true }
  ],
  footerText: "Good luck!",
  timestamp: new Date().toISOString()
};

// Share: localhost:3000/e/giveaway
```

### Example 2: Gaming Event
```javascript
const embed = {
  title: "🎮 Gaming Tournament",
  description: "Join our monthly Valorant tournament!",
  color: "#FF4655",
  alias: "tournament",
  imageUrl: "https://i.imgur.com/banner.png",
  fields: [
    { name: "Date", value: "March 1, 2026", inline: true },
    { name: "Prize Pool", value: "$500", inline: true },
    { name: "Slots", value: "32 teams", inline: true }
  ],
  footerText: "Register now!",
  footerIconUrl: "https://i.imgur.com/logo.png"
};
```

### Example 3: Portfolio Showcase
```javascript
const embed = {
  title: "✨ John's Portfolio",
  description: "Full-stack developer & designer",
  url: "https://john.dev",
  color: "#667eea",
  alias: "john-portfolio",
  thumbnailUrl: "https://github.com/john.png",
  fields: [
    { name: "Skills", value: "React, Node.js, TypeScript", inline: false },
    { name: "Experience", value: "5+ years", inline: true },
    { name: "Projects", value: "50+ completed", inline: true }
  ],
  authorName: "John Doe",
  authorUrl: "https://john.dev",
  authorIconUrl: "https://github.com/john.png",
  footerText: "Available for hire"
};
```

### Example 4: Temporary Link (Auto-Expires)
```javascript
const embed = {
  title: "⏰ Limited Time Offer!",
  description: "50% off - expires in 1 hour",
  color: "#FFA500",
  expiresIn: 3600, // 1 hour in seconds
  redirectUrl: "https://shop.com/sale"
};

// URL auto-expires and redirects users
```

### Example 5: Video Embed
```javascript
const embed = {
  title: "🎬 New Tutorial Video",
  description: "How to build Discord bots",
  videoUrl: "https://youtube.com/watch?v=...",
  thumbnailUrl: "https://img.youtube.com/vi/.../maxresdefault.jpg",
  color: "#FF0000",
  providerName: "YouTube",
  providerUrl: "https://youtube.com"
};
```
> 🔥 **Powerful automation for Discord power users!**

Create stunning embeds directly from Discord with selfbot commands!

### Quick Example
```javascript
// In Discord, type:
.flex Hello world!

// Bot creates instant hidden embed (no visible URL!)
```

### Features
- ✨ **Hidden Embeds** - No visible URL, pure embed
- 🔗 **Visible Embeds** - Shows URL with preview
- 👻 **Stealth Mode** - URL disappears after 2.5s
- ⚡ **Instant Commands** - Type and send
- 🎨 **Full Customization** - All embed features

### Documentation
- 📖 [Complete Selfbot Guide](SELFBOT-GUIDE.md) - Full documentation
- 🚀 [Quick Start Guide](SELFBOT-QUICKSTART.md) - Get started in 5 minutes
- 🇵🇭 [Tagalog Guide](SELFBOT-TAGALOG.md) - Filipino documentation
- 💻 [Example Bot](selfbot-example.js) - Ready-to-use code

### Available Commands
```bash
.flex <text>              # Hidden embed
.link <text>              # Visible embed URL
.stealth <title> | <desc> # URL disappears
.rich <t> | <d> | <img>   # Rich embed
.image <url> <title>      # Image embed
.fields <t> | <n:v> ...   # Embed with fields
```

### ⚠️ Important Warning
**Using selfbots violates Discord's Terms of Service.** Your account may be banned. This is for **educational purposes only**. We are not responsible for any consequences.nouncement) |
| 🆘 Troubleshooting

<details>
<summary><b>Installation fails on Windows (better-sqlite3 error)</b></summary>

We've switched to `sql.js` which doesn't require compilation!

```powershell
# Clean install
Remove-Item -Recurse -Force node_modules
Remove-Item package-lock.json
npm install
```

See [WINDOWS-FIX.md](WINDOWS-FIX.md) for details.

</details>

<details>
<summary><b>Port 3000 already in use</b></summary>

Either kill the process or change the port:

```powershell
# Find what's using port 3000
netstat -ano | findstr :3000

# Kill it (replace PID)
taskkill /PID <PID> /F

# Or change port in .env
PORT=3001
```

</details>

<details>
<summary><b>TypeScript errors</b></summary>

```bash
# Clean rebuild
npm run build

# Check for errors
npm run lint
```

</details>

<details>
<summary><b>Database errors</b></summary>

```powershell
# Delete and recreate database
Remove-Item -Recurse -Force data
npm run dev
```

</details>

## 📖 Documentation Index

| Document | Description |
|----------|-------------|
| [README.md](README.md) | Main documentation (you are here) |
| [QUICKSTART.md](QUICKSTART.md) | Fast setup guide |
| [EXAMPLES.md](EXAMPLES.md) | Code examples (JS, Python, cURL) |
| [STRUCTURE.md](STRUCTURE.md) | Project architecture |
| [SELFBOT-GUIDE.md](SELFBOT-GUIDE.md) | Discord selfbot integration |
| [SELFBOT-QUICKSTART.md](SELFBOT-QUICKSTART.md) | Selfbot quick start |
| [SELFBOT-TAGALOG.md](SELFBOT-TAGALOG.md) | Tagalog selfbot guide |
| [WINDOWS-FIX.md](WINDOWS-FIX.md) | Windows installation fix |
| [CHANGELOG.md](CHANGELOG.md) | Version history |

## 💬 Support & Community

- 🐛 **Found a bug?** [Open an issue](https://github.com/yourusername/webembed/issues)
- 💡 **Have an idea?** [Start a discussion](https://github.com/yourusername/webembed/discussions)
- 📧 **Need help?** Check the docs above or open an issue
- ⭐ **Like the project?** Give us a star on GitHub!

## 🙏 Acknowledgments

- Inspired by [aiko-chan-ai/WebEmbed](https://github.com/aiko-chan-ai/WebEmbed)
- Built with ❤️ for the Discord community
- Special thanks to all contributors!

## 📊 Project Stats

- 📝 **Lines of Code**: ~5,000+
- 📁 **Files**: 25+ source files
- 🧪 **Test Coverage**: API tested
- 🚀 **Performance**: <10ms response time
- 💾 **Database**: SQLite with auto-save

---

<div align="center">

### Made with ❤️ for the Discord community

**[⬆ Back to Top](#-webembed-advanced)**

*If you found this useful, consider giving it a ⭐ star on GitHub!*

</div>
```

#### Response
```json
{
  "success": true,
  "embed": { /* updated embed data */ }
}
```

</details>

<details>
<summary><b>DELETE /api/embeds/:id</b> - Delete embed <i>(requires API key)</i></summary>

#### Request
```bash
curl -X DELETE http://localhost:3000/api/embeds/abc123 \
  -H "X-API-Key: your-api-key"
```

#### Response
```json
{
  "success": true,
  "message": "Embed deleted successfully"
}
```

</details>

<details>
<summary><b>GET /api/embeds</b> - List all embeds <i>(requires API key)</i></summary>

#### Request
```bash
curl http://localhost:3000/api/embeds?limit=10&offset=0 \
  -H "X-API-Key: your-api-key"
```

#### Response
```json
{
  "embeds": [ /* array of embeds */ ],
  "pagination": {
    "limit": 10,
    "offset": 0,
    "count": 10
  }
}
```

</details> "timestamp": "2026-02-18T12:00:00Z"
  }'
```

**Response:**
```json
{
  "success": true,
  "embed": {
    "id": "abc123",
    "alias": "hello",
    "url": "http://localhost:3000/e/hello",
    "shortUrl": "http://localhost:3000/e/hello",
    "oembedUrl": "http://localhost:3000/oembed/abc123",
    "createdAt": 1708257600000
  }
}
```

### View an Embed

**GET** `/e/:idOrAlias`

```bash
# By ID
curl http://localhost:3000/e/abc123

# By alias
curl http://localhost:3000/e/hello
```

### Get Embed Statistics

**GET** `/api/embeds/:id/stats`

Requires API key in `X-API-Key` header.

```bash
curl http://localhost:3000/api/embeds/abc123/stats \
  -H "X-API-Key: your-api-key"
```

**Response:**
```json
{
  "totalViews": 150,
  "uniqueIps": 75,
  "last24Hours": 20,
  "createdAt": 1708257600000
}
```

### Update an Embed

**PUT** `/api/embeds/:id`

Requires API key.

```bash
curl -X PUT http://localhost:3000/api/embeds/abc123 \
  -H "X-API-Key: your-api-key" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Updated Title",
    "description": "New description"
  }'
```

### Delete an Embed

**DELETE** `/api/embeds/:id`

Requires API key.

```bash
curl -X DELETE http://localhost:3000/api/embeds/abc123 \
  -H "X-API-Key: your-api-key"
```

### List All Embeds

**GET** `/api/embeds?limit=50&offset=0`

Requires API key.

```bash
curl http://localhost:3000/api/embeds?limit=10 \
  -H "X-API-Key: your-api-key"
```

## 🔧 Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Server port | `3000` |
| `NODE_ENV` | Environment mode | `development` |
| `ADMIN_API_KEY` | Master API key | (required) |
| `DATABASE_PATH` | SQLite database location | `./data/webembed.sqlite` |
| `CORS_ORIGIN` | CORS allowed origins | `*` |
| `BASE_URL` | Base URL for embeds | `http://localhost:3000` |

### Embed Schema

```typescript
{
  alias?: string;              // Custom short URL (3-50 chars, alphanumeric + _ -)
  title?: string;              // Embed title (max 256 chars)
  description?: string;        // Embed description (max 4096 chars)
  url?: string;                // Link when clicking embed title
  color?: string;              // Hex color (e.g., #FF5733)
  timestamp?: string;          // ISO 8601 timestamp
  imageUrl?: string;           // Large image URL
  thumbnailUrl?: string;       // Thumbnail image URL
  videoUrl?: string;           // Video URL
  providerName?: string;       // Provider name (max 256 chars)
  providerUrl?: string;        // Provider URL
  authorName?: string;         // Author name (max 256 chars)
  authorUrl?: string;          // Author URL
  authorIconUrl?: string;      // Author icon URL
  footerText?: string;         // Footer text (max 2048 chars)
  footerIconUrl?: string;      // Footer icon URL
  fields?: Array<{             // Embed fields (max 25)
    name: string;              // Field name (max 256 chars)
    value: string;             // Field value (max 1024 chars)
    inline?: boolean;          // Display inline
  }>;
  redirectUrl?: string;        // Redirect after viewing
  expiresIn?: number;          // Expiration time in seconds
}
```

## 🎯 Use Cases

- **Discord Server Welcomes**: Create beautiful welcome messages with embeds
- **Portfolio Links**: Showcase your work with rich previews
- **Announcements**: Share important updates with styled embeds
- **Event Invites**: Create attractive event announcements
- **Link Shortening**: Shorten URLs while adding Discord previews
- **Marketing**: Create branded links with custom embeds

## 📊 Database

The application uses SQLite with Write-Ahead Logging (WAL) for optimal performance. The database includes:

- **embeds**: Stores all embed configurations
- **analytics**: Tracks embed views and interactions
- **api_keys**: Manages API key authentication

### Automatic Cleanup

Expired embeds are automatically cleaned up every hour.

## 🔒 Security Features

- **Rate Limiting**: Global and endpoint-specific rate limits
- **API Key Authentication**: Secure protected endpoints
- **Helmet.js**: Security headers
- **Input Validation**: Zod schema validation
- **CORS Protection**: Configurable CORS policies

## 🧪 Development

```bash
# Install dependencies
npm install

# Run in development mode with auto-reload
npm run dev

# Build TypeScript
npm run build

# Run linter
npm run lint

# Format code
npm run format
```

## 📝 Scripts

- `npm run dev` - Start development server with auto-reload
- `npm run build` - Build TypeScript to JavaScript
- `npm start` - Start production server
- `npm run lint` - Run ESLint
- `npm run format` - Format code with Prettier
- `npm run db:migrate` - Run database migrations

## 🚢 Production Deployment

### Using PM2

```bash
npm install -g pm2
npm run build
pm2 start dist/index.js --name webembed
pm2 save
pm2 startup
```

### Using Docker

See the [Docker Deployment](#docker-deployment) section above.

### Environment Setup

1. Set `NODE_ENV=production`
2. Use a strong `ADMIN_API_KEY`
3. Set proper `BASE_URL` to your domain
4. Configure `CORS_ORIGIN` to restrict access
5. Use a reverse proxy (nginx/Caddy) for SSL

## � Discord Selfbot Integration

Want to use embeds with Discord selfbots? Check out [SELFBOT-GUIDE.md](SELFBOT-GUIDE.md) for:
- Hidden embeds (no visible URL)
- Non-hidden embeds (with URL)
- Stealth mode (URL disappears after embed loads)
- Complete selfbot example with commands

⚠️ **Warning**: Using selfbots violates Discord's Terms of Service. Use at your own risk.

## �🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

MIT License - see LICENSE file for details

## 🙏 Credits

Inspired by the original [WebEmbed](https://github.com/aiko-chan-ai/WebEmbed) by aiko-chan-ai, but completely rewritten with modern features and improvements.

## 💬 Support

If you have questions or need help, please open an issue on GitHub.

---

Made with ❤️ for the Discord community
