# Bruno Barreto — Portfolio Site

![Status](https://img.shields.io/badge/status-live-success)
![Hosting](https://img.shields.io/badge/hosting-AWS%20Amplify-orange)
![Stack](https://img.shields.io/badge/stack-HTML%20%7C%20CSS%20%7C%20JS-blue)

Public portfolio showcasing three proprietary projects in automation and artificial intelligence: Jarvis, ContentFlow AI, and NEXUS.

## 🔗 Live Site

**Production:** [https://main.d224tz0vfoxquk.amplifyapp.com/](https://main.d224tz0vfoxquk.amplifyapp.com/)

## 📄 Pages

| Page | URL | Description |
|------|-----|-------------|
| **Home** | `/index.html` | Portfolio overview with project highlights and metrics |
| **Jarvis** | `/jarvis.html` | Personal cognitive infrastructure system |
| **ContentFlow AI** | `/contentflow.html` | Automated content production pipeline |
| **NEXUS** | `/nexus.html` | B2B sales intelligence and outbound automation |

## 🏗️ Architecture

```
GitHub → Amplify (CI/CD) → CloudFront (CDN) → Browser
```

The site is deployed via AWS Amplify with automatic CI/CD from the `main` branch. CloudFront provides global CDN distribution for optimal performance.

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | HTML5, CSS3, JavaScript | Static site with responsive design |
| **Storage** | AWS S3 | Asset storage and origin |
| **CI/CD** | AWS Amplify | Automated deployment pipeline |
| **CDN** | CloudFront | Global content delivery |
| **Video** | MP4 embeds | Hero backgrounds and presentations |
| **Cost** | ~$0/month | Static hosting with minimal traffic |

## 💡 Design Decisions

- **Pure static site**: No frameworks (React, Next.js) to maintain simplicity and performance
- **Amplify CI/CD**: Automatic deployment on every push to `main` branch
- **Unified visual identity**: Consistent design language across all project pages
- **Near-zero operational cost**: Static hosting optimized for minimal AWS charges

## 🚀 Local Development

No build step required. Simply open `index.html` in your browser:

```bash
# Clone the repository
git clone https://github.com/BrunoBarreto91/pentecost-site.git
cd pentecost-site

# Open in browser
open index.html  # macOS
start index.html # Windows
xdg-open index.html # Linux
```

Or use a local server:

```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve
```

## 📦 Deploy

Deployment is fully automated via AWS Amplify:

1. Push changes to `main` branch
2. Amplify detects the commit
3. Builds and deploys automatically
4. CloudFront cache invalidation triggered

For detailed deployment setup, see [`docs/deploy.md`](docs/deploy.md).

## 🔗 Related Projects

- **[Jarvis](https://github.com/BrunoBarreto91/Jarvis)** — Personal cognitive infrastructure
- **[ContentFlow-AI](https://github.com/BrunoBarreto91/ContentFlow-AI)** — Automated content production pipeline
- **NEXUS** — B2B sales intelligence (private repository)

## 📧 Contact

**Bruno Barreto**  
Automation, AI & Systems Architecture

- **GitHub:** [github.com/BrunoBarreto91](https://github.com/BrunoBarreto91)
- **LinkedIn:** [linkedin.com/in/brunobarreto91](https://linkedin.com/in/brunobarreto91)
- **Email:** brunocesar1291@gmail.com

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details.

---

**Built with:** HTML5, CSS3, JavaScript, AWS Amplify, CloudFront
