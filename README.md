# MediaStream App Store

A custom Umbrel app store featuring a complete media streaming solution.

## What's Included

This app store contains the **Jellyfin Media Stack** - a complete media streaming solution that includes:

- **Zurg**: Efficient debrid service integration for Real-Debrid
- **RClone**: Cloud storage mounting with advanced caching
- **Jellyfin**: Feature-rich media server with hardware acceleration

## How to Add This App Store to Umbrel

1. Open your Umbrel dashboard
2. Navigate to the App Store
3. Click on "Community App Stores" or the settings icon
4. Add the GitHub URL of this repository
5. The MediaStream app store will appear with the Jellyfin Media Stack app

## App Configuration

### Zurg Configuration

After installation, you'll need to configure Zurg with your Real-Debrid credentials:

1. Create a `config.yml` file in the Zurg config directory
2. Add your Real-Debrid API token
3. Configure your preferred settings

Example `config.yml`:
```yaml
# Zurg configuration
token: YOUR_REAL_DEBRID_API_TOKEN
```

### RClone Configuration

RClone is pre-configured to mount the Zurg remote to `/data`. The configuration includes:
- VFS caching for smooth playback
- 100GB cache size (adjustable in docker-compose.yml)
- Optimized settings for media streaming

### Jellyfin Setup

1. After installation, access Jellyfin at `http://umbrel.local:8096`
2. Complete the initial setup wizard
3. Add your media library pointing to `/media`
4. Configure hardware acceleration if available:
   - Intel Quick Sync (pre-configured)
   - NVIDIA (requires additional setup)
   - AMD (requires additional setup)

## Hardware Acceleration

The stack includes support for Intel Quick Sync hardware acceleration out of the box. The following devices are mapped:
- `/dev/dri/renderD128`
- `/dev/dri/card0`

For NVIDIA or AMD GPUs, you'll need to modify the docker-compose.yml accordingly.

## Ports

- **8096**: Jellyfin web interface
- **8920**: Jellyfin HTTPS (if configured)
- **9999**: Zurg API
- **7359/udp**: Jellyfin service discovery
- **1900/udp**: Jellyfin DLNA

## Volume Mappings

All data is stored in the app's data directory:
- `zurg/config`: Zurg configuration files
- `zurg/data`: Zurg data and cache
- `rclone/config`: RClone configuration
- `rclone/logs`: RClone logs
- `jellyfin/config`: Jellyfin configuration
- `jellyfin/cache`: Jellyfin cache
- `media`: Mounted media from RClone (shared between services)

## Troubleshooting

### RClone mount not working
- Check RClone logs in the data directory
- Verify Zurg is running and accessible
- Ensure proper permissions for mounting

### Hardware acceleration not working
- Verify your GPU drivers are installed
- Check that the render group (109) matches your system
- Review Jellyfin dashboard for hardware acceleration status

### Performance issues
- Adjust VFS cache size in docker-compose.yml
- Increase cache directory space
- Check network bandwidth between debrid service and your Umbrel

## Support

For issues and questions:
- Zurg: https://github.com/debridmediamanager/zurg-testing/discussions
- Jellyfin: https://jellyfin.org/docs/
- RClone: https://rclone.org/docs/

## License

This app store configuration is provided as-is. Individual components (Zurg, RClone, Jellyfin) are subject to their respective licenses.
