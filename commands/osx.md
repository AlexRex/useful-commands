# OS X

#### Remove all .DS_STORE files in a folder.
```bash
find . -name '.DS_Store' -type f -delete
```

#### Kill JamSoftware

```bash
sudo launchctl unload /Library/LaunchDaemons/com.jamfsoftware.jamf.daemon.plist
sudo launchctl unload -w /Library/LaunchDaemons/com.jamfsoftware.startupItem.plist
sudo launchctl unload -w /Library/LaunchDaemons/com.jamfsoftware.task.1.plist
```