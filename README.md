# MultistreamLabels

Combine YouTube memberships, Twitch subscribers, and Kick subscribers into unified session goals for your stream overlays.

## Features

- 🔗 **Multi-Platform Integration**: Connect YouTube, Twitch, and Kick accounts
- 🔐 **OAuth Authentication**: Secure, automated token authentication with auto-refresh
- 🎯 **Customizable Goals**: Set combined or per-platform subscription goals
- 📁 **OBS-Ready Labels**: Auto-updating text files for OBS Text sources
- 🔄 **Real-Time Updates**: Live dashboard with Socket.IO
- 📊 **Session Tracking**: Track subscriptions per session with manual reset
- 💰 **Tier-Based Points**: T1 = 1pt, T2 = 2pts, T3 = 6pts (like Twitch sub points)
- 🧪 **Auto-Detection Simulator**: Test your setup without real subscribers
- 💾 **Persistent Data**: Session data survives app restarts

## Quick Start

1. Run MultistreamLabels Setup 1.0.2.exe in /dist and install the program
2. Run MultistreamLabels 1.0.2.exe in the /dist/win-unpacked folder
3. Configure your OAuth credentials in the app
4. Connect your platforms and start streaming!

When you first launch the app, you'll need to configure your OAuth credentials:

### Twitch Setup

1. Go to [Twitch Developer Console](https://dev.twitch.tv/console/apps)
2. Click "Register Your Application"
3. Fill in:
   - Name: MultistreamLabels (or your choice)
   - OAuth Redirect URLs: `http://localhost:3000/auth/twitch/callback`
   - Category: Broadcasting Suite
4. Copy the **Client ID** and generate a **Client Secret**
5. In the app, scroll to "API Configuration" and enter your credentials
6. Click "Save Twitch Credentials"
7. Click "Connect" next to Twitch

### YouTube Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable the **YouTube Data API v3**
4. Go to Credentials → Create Credentials → OAuth client ID
5. Configure the OAuth consent screen if prompted
6. Set Application type to "Web application", and set it to External
7. Add authorized redirect URI: `http://localhost:3000/auth/youtube/callback`
8. Copy the **Client ID** and **Client Secret**
9. In the app, scroll to "API Configuration" and enter your credentials
10. Click "Save YouTube Credentials"
11. Go to the "Audience" section in the Google Auth Platform and Publish the app.
11. Click "Connect" next to YouTube and log in to your YouTube account

**Note**: YouTube membership data requires your channel to be in the YouTube Partner Program with memberships enabled.

### Kick Setup

Kick doesn't currently have a public OAuth API. You can:
- Enter your channel slug in the dashboard
- Add subscribers manually via the Manual Entry section

## Tier Points System

The app uses a point-based system like Twitch's sub points:

| Tier | Points |
|------|--------|
| Tier 1 | 1 point |
| Tier 2 | 2 points |
| Tier 3 | 6 points |

**YouTube Membership Tiers**: Automatically mapped by level order:
- 1st membership level = T1 (1 pt)
- 2nd membership level = T2 (2 pts)  
- 3rd+ membership level = T3 (6 pts)

## Using with OBS

The application generates text files in the `labels/` folder that auto-update:

| File | Description |
|------|-------------|
| `combined_count.txt` | Total subscribers across all platforms |
| `combined_points.txt` | Total points (tier-weighted) |
| `combined_goal.txt` | Combined goal target |
| `combined_progress.txt` | "X / Y" format |
| `combined_labeled_progress.txt` | "Sub Goal: X / Y" format |
| `combined_percentage.txt` | Percentage complete |
| `combined_remaining.txt` | Remaining to goal |
| `twitch_count.txt` | Twitch subscriber count |
| `youtube_count.txt` | YouTube member count |
| `kick_count.txt` | Kick subscriber count |
| `latest_subscriber.txt` | Most recent subscriber |

### Adding to OBS

1. Add a **Text (GDI+)** source
2. Check "Read from file"
3. Browse to select the label file from the `labels/` folder
4. The text will auto-update as your counts change

**Labels folder location:**
- Portable app: `C:\Users\<YourName>\AppData\Roaming\MultistreamLabels\labels\`
- From source: `./labels/` in the project folder

## Data Storage

All data is stored persistently in:
- **Windows**: `C:\Users\<YourName>\AppData\Roaming\MultistreamLabels\data\`

This includes:
- `session.json` - Current session counts and events
- `auth.json` - OAuth tokens (auto-refreshed)
- `credentials.json` - Your OAuth app credentials
- `settings.json` - App settings

## Building from Source

```bash
# Build Windows portable exe
npm run build:win
```

Output: `dist/MultistreamLabels 1.0.1.exe`

## Troubleshooting

### OAuth Errors

- Ensure redirect URIs match exactly: `http://localhost:3000/auth/twitch/callback`
- Check that client ID and secret are correctly entered
- For YouTube, ensure your channel is in the Partner Program

### Labels Not Updating

- Check the labels folder path in the app dashboard
- Verify the server is running (check the connection status)
- Try clicking "Open Labels Folder" to verify the path

### YouTube 403 Error

- Make sure you've enabled the **YouTube Data API v3** in Google Cloud Console
- Check that your OAuth consent screen is configured

### Platform Not Configured Error

- You need to enter your OAuth credentials in the "API Configuration" section before connecting

## License

MIT License
