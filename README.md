# Huntarr Docker Stack

Music discovery and organization tool that integrates with Lidarr to automatically find and add new music to your collection.

## Quick Start

```bash
cp .env.example .env
# Edit .env to match your system
docker-compose up -d
```

Access the web interface at: http://localhost:9705

## What is Huntarr?

Huntarr is a music discovery tool that helps expand your music collection by:
- **Discovering** new artists and albums based on your preferences
- **Integrating** with Lidarr to automatically add discovered music
- **Tracking** music trends and popular releases
- **Suggesting** similar artists and genres you might enjoy

## Configuration

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `PUID` | 1000 | User ID for file permissions |
| `PGID` | 1000 | Group ID for file permissions |
| `TZ` | America/New_York | Timezone |
| `HUNTARR_PORT` | 9705 | Web interface port |

### Directory Structure

```
huntarr/
└── config/     # Huntarr configuration and database (auto-created)
```

## Initial Setup

### 1. Access Web Interface
Navigate to http://localhost:9705 and complete the initial setup.

### 2. Configure Music Services
Connect Huntarr to your music discovery services:

**Spotify Integration:**
- Connect your Spotify account for playlist analysis
- Import your liked songs and playlists
- Discover similar artists and tracks

**Last.fm Integration:**
- Connect your Last.fm account for scrobbling data
- Analyze your listening history
- Get personalized recommendations

**Apple Music/Other Services:**
- Configure additional music services if supported
- Import playlists and listening data

### 3. Configure Lidarr Integration
Connect Huntarr to your Lidarr instance:
- **Lidarr URL**: `http://lidarr:8686` (if using Docker networks) or `http://localhost:8686`
- **API Key**: Get from Lidarr → Settings → General
- **Quality Profile**: Select default quality for auto-added music
- **Monitor Options**: Configure how new artists should be monitored

### 4. Set Discovery Preferences
Configure your music discovery preferences:
- **Genres**: Select preferred and avoided genres
- **Release Types**: Albums, EPs, Singles, etc.
- **Quality Thresholds**: Minimum quality requirements
- **Auto-Add Settings**: Automatic vs. manual approval

## Features

### Music Discovery
- **Similar Artist Discovery**: Find artists similar to your favorites
- **Genre Exploration**: Discover new genres and subgenres
- **Trending Music**: Stay up-to-date with popular releases
- **Chart Integration**: Billboard, iTunes, Spotify charts

### Playlist Analysis
- **Spotify Playlists**: Analyze your playlists for discovery patterns
- **Collaborative Playlists**: Discover music from shared playlists
- **Mood-Based Discovery**: Find music matching specific moods

### Integration Features
- **Auto-Add to Lidarr**: Automatically add discovered artists
- **Quality Control**: Filter discoveries by quality preferences
- **Duplicate Detection**: Avoid adding music you already have
- **Batch Operations**: Bulk add/remove discovered music

## Integration with Lidarr

### Automatic Artist Addition
1. Huntarr discovers new artists based on your preferences
2. Artists are automatically added to Lidarr (if enabled)
3. Lidarr monitors and downloads the artist's discography
4. New releases are automatically tracked

### Manual Review Process
1. Huntarr presents discovered artists for review
2. You approve/reject artists manually
3. Approved artists are added to Lidarr
4. Quality profiles and monitoring are applied

## Discovery Sources

### Streaming Services
- **Spotify**: Playlists, related artists, recommendations
- **Apple Music**: Personal recommendations and charts
- **YouTube Music**: Trending and recommended content

### Music Databases
- **MusicBrainz**: Artist relationships and metadata
- **Last.fm**: Similar artists and listening data
- **AllMusic**: Genre classifications and reviews

### Social Sources
- **Reddit**: Music subreddits and community recommendations
- **RateYourMusic**: User ratings and charts
- **Bandcamp**: Independent artist discovery

## Troubleshooting

### Cannot Connect to Music Services
- Verify API credentials are correct
- Check if services require re-authentication
- Review rate limiting and quota restrictions
- Test connectivity from container

### Lidarr Integration Issues
- Verify Lidarr API key is correct
- Check network connectivity between containers
- Ensure Lidarr is accessible from Huntarr
- Review Lidarr logs for connection errors

### Discovery Not Working
- Check configured discovery sources
- Verify service authentications are active
- Review discovery preferences and filters
- Check for rate limiting or API restrictions

### Duplicate Artists Being Added
- Enable duplicate detection in settings
- Verify Lidarr integration is working properly
- Check artist matching algorithms
- Review manual approval process

## Security Notes

- Secure API keys for all connected services
- Use OAuth authentication where available
- Regularly review connected applications
- Keep Huntarr updated for security patches

## Performance Tips

- Configure reasonable discovery intervals
- Use filters to reduce processing load
- Monitor API usage and rate limits
- Regularly clean up old discovery data

## Backup

Important directories to backup:
- `./config` - Contains all Huntarr settings and discovery data

```bash
tar -czf huntarr-backup-$(date +%Y%m%d).tar.gz config/
```

## Advanced Configuration

### Custom Discovery Sources
- Configure additional RSS feeds
- Add custom music blogs and websites
- Set up webhook integrations
- Create custom discovery algorithms

### API Integration
- Use Huntarr's API for custom integrations
- Automate discovery processes
- Create custom dashboards
- Build notification systems

## Updates

```bash
docker-compose pull
docker-compose up -d
docker image prune
```

## Workflow Examples

### Spotify Playlist Discovery
1. Connect Spotify account to Huntarr
2. Import your favorite playlists
3. Huntarr analyzes tracks and finds similar artists
4. New artists automatically added to Lidarr
5. Lidarr downloads new music automatically

### Genre Exploration
1. Set target genre in Huntarr preferences
2. Configure discovery sources for that genre
3. Review suggested artists manually
4. Approve interesting discoveries
5. Monitor new releases from approved artists

### Social Discovery
1. Connect Last.fm and other social services
2. Import listening history and scrobbles
3. Find friends and similar users
4. Discover music from similar taste profiles
5. Add discoveries to your collection automatically