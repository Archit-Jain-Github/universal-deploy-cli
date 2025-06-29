# Universal Deploy CLI Tool

A comprehensive command-line tool for deploying full-stack applications to multiple platforms with a single command.

## 🚀 Supported Platforms

- **Vercel** - Fast deployments with edge functions
- **Cloudflare Pages** - Global CDN with edge computing
- **Netlify** - JAMstack deployments with form handling

## 📦 Supported Project Types

- Next.js applications
- React applications
- Vue.js applications
- Nuxt.js applications
- Svelte applications
- Static HTML sites
- Node.js applications
- Docker applications
- Custom projects

## 🛠️ Features

- **Interactive CLI** - Guided deployment process
- **Auto-detection** - Automatically detects project type and suggests build settings
- **Multi-platform** - Deploy to Vercel, Cloudflare Pages, or Netlify
- **Customizable** - Override default build settings
- **Global command** - Access from anywhere with `deploy` command
- **Authentication** - Handles platform authentication automatically
- **Status checking** - Monitor deployment status
- **Configuration files** - Auto-generates platform-specific config files

## 📋 Prerequisites

- macOS (tested on macOS)
- Node.js (v14 or higher)
- npm or yarn
- Git

## 🔧 Installation & Setup

### Step 1: Clone the Repository

```bash
# Create a directory for the deploy tool
mkdir -p ~/deploy-cli
cd ~/deploy-cli

# Clone the repository
git clone https://github.com/Archit-Jain-Github/universal-deploy-cli.git
```

### Step 2: Make the Script Executable

```bash
chmod +x deploy
```

### Step 3: Create Global Command Directory

```bash
# Create a directory for custom commands
mkdir -p ~/.local/bin

# Copy the deploy script to the global directory
cp deploy ~/.local/bin/deploy

# Make sure the script is executable
chmod +x ~/.local/bin/deploy
```

### Step 4: Update PATH Environment Variable

Add the custom commands directory to your PATH:

```bash
# For Zsh (default on macOS)
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

# For Bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
```

### Step 5: Verify Installation

```bash
# Check if the command is available globally
which deploy

# Should output: /Users/yourusername/.local/bin/deploy

# Test the command
deploy --version
```

## 🎯 Usage

### Basic Usage

```bash
# Interactive deployment (recommended for first-time users)
deploy

# Deploy to specific platform
deploy -p vercel
deploy -p cloudflare
deploy -p netlify

# Check deployment status
deploy --status -p vercel

# Show help
deploy --help
```

### Command Options

```bash
deploy [OPTIONS]

Options:
  -h, --help         Show help message
  -v, --version      Show version information
  -s, --status       Show deployment status
  -p, --platform     Specify platform (vercel, cloudflare, netlify)
```

### Examples

```bash
# Deploy a React app to Vercel
cd my-react-app
deploy -p vercel

# Deploy a Next.js app to Cloudflare Pages
cd my-nextjs-app
deploy -p cloudflare

# Deploy a static site to Netlify
cd my-static-site
deploy -p netlify

# Check status of all deployments
deploy --status -p vercel
deploy --status -p cloudflare
deploy --status -p netlify
```

## 🔐 Authentication

The tool will automatically handle authentication for each platform:

### Vercel

- Runs `vercel login` if not authenticated
- Opens browser for OAuth authentication

### Cloudflare Pages

- Prompts for API token if not authenticated
- Get token from: https://dash.cloudflare.com/profile/api-tokens
- Requires "Cloudflare Pages:Edit" permission

### Netlify

- Runs `netlify login` if not authenticated
- Opens browser for OAuth authentication

## 📁 Configuration Files

The tool automatically creates platform-specific configuration files:

### Vercel (`vercel.json`)

```json
{
  "version": 2,
  "builds": [
    {
      "src": "**/*",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "build"
      }
    }
  ]
}
```

### Cloudflare Pages (`wrangler.toml`)

```toml
name = "my-project"
compatibility_date = "2023-12-01"

[env.production]
account_id = ""
pages_build_output_dir = "dist"
```

### Netlify (`netlify.toml`)

```toml
[build]
  command = "npm run build"
  publish = "build"

[build.environment]
  NODE_VERSION = "18"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

## 🔄 Updating the Tool

To update the deployment tool:

```bash
cd ~/deploy-cli
git pull origin main
cp deploy ~/.local/bin/deploy
chmod +x ~/.local/bin/deploy
```

## 🐛 Troubleshooting

### Command not found

```bash
# Check if PATH is set correctly
echo $PATH | grep -q "$HOME/.local/bin" && echo "PATH is set" || echo "PATH not set"

# Reload shell configuration
source ~/.zshrc  # or ~/.bash_profile
```

### Permission denied

```bash
# Make sure the script is executable
chmod +x ~/.local/bin/deploy
```

### CLI tools not found

The script will automatically install required CLI tools:

- Vercel CLI: `npm install -g vercel`
- Wrangler CLI: `npm install -g wrangler`
- Netlify CLI: `npm install -g netlify-cli`

### Authentication issues

```bash
# Clear authentication and re-authenticate
vercel logout && vercel login
netlify logout && netlify login
wrangler logout && wrangler login
```

## 📝 Development

### Directory Structure

```
universal-deploy-cli/
├── deploy              # Main deployment script
├── README.md          # This file
├── .gitignore         # Git ignore file
└── examples/          # Example projects
    ├── react-app/
    ├── nextjs-app/
    └── static-site/
```

### Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

MIT License - see LICENSE file for details

## 🆘 Support

If you encounter any issues:

1. Check the troubleshooting section
2. Review the platform-specific documentation:
   - [Vercel Documentation](https://vercel.com/docs)
   - [Cloudflare Pages Documentation](https://developers.cloudflare.com/pages)
   - [Netlify Documentation](https://docs.netlify.com)
3. Open an issue on GitHub

## 🎉 Success!

You should now be able to deploy any full-stack application using the `deploy` command from anywhere in your terminal!
