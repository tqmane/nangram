# Nangram User Guide

[日本語ユーザーガイド](../jp/GUIDE.md) | [Documentation Index](README.md) | [Releases](https://github.com/tqmane/nangram/releases) | [Support Discord](https://discord.gg/zJBrCaf6dz)

This guide provides setup instructions, feature overviews, and operational guidance for **Nangram**.

> [!NOTE]
> Nangram is an independent Android customization module developed independently of Instagram and Meta. It is neither affiliated with nor endorsed by Instagram or Meta.

---

## 1. System Requirements & Compatibility

Verify your device environment satisfies these prerequisites before proceeding:

* **Framework Requirement**: Requires an Android module environment supporting **libxposed API 102** as a necessary setup requirement.
* **Module Manager**: Must support scoping modules to specific applications. Not all managers or patching utilities work.
* **Patch-Embedded Installations**: If using an environment that patches the module directly into an APK, you must re-patch and re-install after module updates according to your manager's workflow.
* **Compatibility**: Instagram version `453.0.0.0.45` startup and settings have been checked, though not all features are verified. Version `452.0.0.0.7` is not verified on device. Refer to release notes for compatibility updates.
* **Signing Keys & Data**: Updates require APKs signed with the same signing key. Local data belongs to each app separately: uninstalling Nangram removes its own companion data, while uninstalling Instagram removes data stored within Instagram. Always back up important data and verify your signing key before any uninstallation; do not casually uninstall either app.

---

## 2. Installation & Initial Setup

Follow this step-by-step procedure:

1. **Install Module APK**: Download an official signed Nangram APK when published on [GitHub Releases](https://github.com/tqmane/nangram/releases). Install it via the Android package installer.
2. **Enable and Set Scope**: Open your module manager, enable Nangram, and check **Instagram** in its application scope.
3. **Restart Instagram**: Force stop Instagram in Android settings (`Settings > Apps > Instagram > Force Stop`), then open it.
4. **Initial Preparation**: Open Instagram after enabling or updating the module and wait briefly for setup tasks to finish.
5. **Access In-App Settings**: Long-press the **Home tab** in the Instagram bottom navigation bar to open the in-app Nangram configuration screen.

---

## 3. Companion Dashboard & Settings Synchronization

Tapping the Nangram launcher icon opens the companion dashboard directly without extra launch prompts.

* **Connection Status**: Displays the live communication state with Instagram. Tap the **Open Instagram** button if Instagram is not running.
* **Search Capabilities**: Filter and find settings by searching feature names, descriptions, or setting keys.
* **Documentation Links**: In-app guide links route based on the app's current display language (not the device language): Japanese routes to `jp`, and all other languages route to `en`.
* **Frequently Used Settings**: Customize up to six quick shortcuts on the dashboard:
  1. Tap **Choose displayed settings** to open the selection screen.
  2. Search and select up to six options using the checkboxes (the selection count is displayed).
  3. Tap **Save selection** to apply, or **Cancel** to discard changes.
  * *Note*: This configures dashboard shortcuts only; it does not turn underlying features on or off.
* **Settings Synchronization**: Settings synchronize with Instagram while connected. Some features require restarting Instagram to take effect. If disconnected, open Instagram and verify module scope. The companion dashboard provides search, shortcuts, connection status, and help links. Media downloads, message history, and backup tools are managed within Nangram settings inside Instagram.

---

## 4. Feature Groups & Operational Details

Features can be enabled individually when supported. Availability may vary by Instagram version, account status, or device characteristics.

### Feed & Interactions
* **Feed Filtering**: Hide sponsored posts, suggestions, or reels from your main feed.
* **Content Copying**: Copy captions, comments, and profile bios to the clipboard.
* **Photo Zoom**: Zoom photos with touch gestures.
* **Action Confirmations**: Prevent accidental likes, follows, or comments with confirmation prompts before actions run.

### Stories & Personal Archives
* **Playback Controls & Ghost Viewing**: Use playback controls and browse stories without sending seen indicators on supported screens when the feature is active.
* **Viewed Stories vs. Own Story Archive**:
  * *Viewed stories*: Save other users' stories upon request when viewing them.
  * *Own posted-story archive*: Locally stores personal stories and viewer lists fetched while active. Previously expired stories cannot be recovered.
* **Foreground Execution**: Automated story archives and checks run only while Instagram is active in the foreground under the current account. Scheduled background automation is not supported.

### Direct Messages & Privacy
* **Ghost Read**: Prevents sending read receipts for messages you view while the feature is supported and active.
* **Manual Receipts**: Using the manual receipt action sends a read receipt to the server (delivery depends on connection and server response, without instant-success guarantees).
* **Message Retention**: Records incoming messages and retains unsent or deleted messages observed while active. Messages deleted before enabling the feature cannot be recovered.
* **Local Locks**: Protects conversation views and Nangram settings with local biometric or PIN locks. These locks secure local screens only, not the server-side account.

### Media Downloads & Library
* **Storage Destination**: Select a download folder via the Android system storage picker.
* **Download Actions**: Save media using action buttons embedded in posts, reels, or stories.
* **Queue Management**: The queue shows progress and failure status with cancel and retry options.
* **Expired Media URLs**: If a media link expires, reopen the post in Instagram to refresh it. Unavailable or deleted media cannot be recovered.
* **Profile Bulk Downloads**: Download media from profiles in batches using preset counts, custom counts, or all. Downloads process step by step; if stopped by connection loss, rate limits, or storage limits, already queued items remain.
* **Media Library**: Organize downloads with name search, type filters, folders, and favorites. External copies exported to galleries or shared outside remain intact during library cleanup.

### Profile Watchlists & Appearance
* **Watchlists**: Track bio, avatar, and follower changes while Instagram runs in the foreground under the active account.
* **Appearance & Profiles**: Customize themes and switch between configuration profiles linked to specific accounts.

---

## 5. Storage, Retention & Backups

Configure local data retention policies and create portable backups:

* **Storage Limits**: Configure maximum download file sizes and retention periods (`0` indicates unlimited size or no expiry).
* **Capacity Limit Behavior**: Reaching storage capacity stops new saves instead of automatically deleting existing files.
* **Retention Cleanup**: Retention rules remove older files, with an option to preserve favorites. Exported gallery copies remain unaffected.
* **Backup Creation**: Export settings and local records to a ZIP archive via the Android file picker. Choose whether to include media. The ZIP is unencrypted, so store it privately.
* **Backup Contents & Exclusions**: The backup contents depend on whether you include media. A separate settings-only JSON export contains configuration only and is not a full backup. Backups **never** include account passwords, session tokens, or local lock credentials.
* **Local History Observation**: Local message history and story archives are recorded only while the respective feature is active and data is observed. Content deleted or expired before enabling cannot be recovered.
* **Restoring**: Select a backup ZIP through the file picker. Restoration applies on the **next Instagram start** without requiring a device reboot.

---

## 6. Troubleshooting & Support

| Issue | Cause | Resolution |
| :--- | :--- | :--- |
| **No Connection** | Module inactive or incorrect scope | 1. Confirm module is enabled in manager.<br>2. Verify Instagram is checked in scope.<br>3. Force stop and restart Instagram.<br>4. Ensure your manager supports libxposed API 102. |
| **Setting Ineffective** | Restart required or version mismatch | 1. Force stop and restart Instagram (some settings require restarting Instagram).<br>2. Confirm Instagram version compatibility. |
| **Save Failed** | Permission, capacity, or expired URL | 1. Verify folder write permissions in Android storage.<br>2. Confirm available disk capacity.<br>3. Revisit the post in Instagram to refresh media links. |
| **Update Failed** | Package signing key mismatch | 1. Use an APK signed with the exact same signing key.<br>2. Back up data before attempting updates.<br>3. If patch-embedded, re-patch with your manager. |

### Diagnostic Reporting
When requesting help in the [Discord Community](https://discord.gg/zJBrCaf6dz), provide:
1. Nangram version, Instagram version, Android release, and device model.
2. Clear reproduction steps.
3. Sanitized diagnostic logs exported from the companion app.
4. **Never share passwords, session tokens, private message text, or unredacted personal screenshots.**
