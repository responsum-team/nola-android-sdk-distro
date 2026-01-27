# ResChat SDK

SDK for embedding the Responsum ChatBot in your Android apps.

> **Latest version:** 1.1.1

---

## Features

- **One-line integration** — launch the full chat UI with a single call.  
- **WebSocket-powered chat** — real-time, bidirectional messaging with configurable endpoints.  
- **Fully themable** — override colors, icons, and navigation bar appearance.  
- **Customizable configuration** — predefine session values like airport, language, and location for a tailored chat experience.

---

## Requirements

- Android SDK 28+

---

## Installation

### Step 1: Add JitPack Repository

In your root `build.gradle` (inside `dependencyResolutionManagement`):

```kotlin
dependencyResolutionManagement {
    repositories {
        // ... other repositories
        maven { url 'https://jitpack.io' }
    }
}
```

### Step 2: Add the Dependency

In your module's `build.gradle.kts`:

```kotlin
dependencies {
    implementation("com.github.responsum-team:nola-android-sdk-distro:1.1.1@aar")
    implementation("com.github.responsum-team:nola-android-sdk-distro:1.1.1")
}
```

---

## Quick Start

```kotlin
//"this" is Context parameter
ResChat.startChat(this)
```

This opens the chat screen with default UI and prompts the user to select airport and language.

---

## Customization & Theming

The SDK supports theming via three customization classes: `ColorCustomization`, `ImageCustomization`, and `NavigationBarCustomization`.

### Color Customization

```kotlin
val customColors = ColorCustomization(
    chatBotAvatarBackgroundColor = Color.Red,
    userAvatarBackgroundColor = Color.Green,
    backgroundColor = Color.Blue,
    botChatBubbleBackgroundColor = Color.Yellow,
    timestampTextColor = Color.Magenta,
    messageTextColor = Color.Cyan,
    inputFieldPlaceholderTextColor = Color.Gray,
    inputFieldBorderColor = Color.Black,
    botChatBubbleShadowColor = Color.Cyan,
    sendIconColor = Color.Red,
    microphoneIconColor = Color.White,
    textColor = Color.Black,
    settingsInputButtonsBackgroundColor = Color.Black,
    settingsInputButtonsTextActiveColor = Color.Green,
    settingsInputButtonsTextInactiveColor = Color.Gray,
    settingsStartChatBackgroundColor = Color.Gray,
    settingsStartChatTextColor = Color.White
)
```

### Image Customization

```kotlin
val customImages = ImageCustomization(
    chatBotIcon = R.drawable.custom_bot_icon,
    userIcon = R.drawable.custom_user_icon,
    sendIcon = R.drawable.custom_send_icon,
    microphoneIcon = R.drawable.custom_mic_icon
)
```

### Navigation Bar Customization

```kotlin
val customNavigationBar = NavigationBarCustomization(
    title = "Custom HelpBot",
    font = TextStyle(
        fontSize = 20.sp,
        fontWeight = FontWeight.SemiBold
    ),
    backgroundColor = Color.Gray,
    textColor = Color.White,
    backButtonColor = Color.Red,
    backButtonImage = R.drawable.custom_back_button,
    cleanButtonImage = R.drawable.custom_clean_button
)
```

### Applying Customization

```kotlin
ResChat.startChat(
    context = this,
    colorCustomization = customColors,
    imageCustomization = customImages,
    navigationBarCustomization = customNavigationBar
)
```

---

## Configuration

### API Parameters

| Parameter     | Description                                  | Default                                 |
|---------------|----------------------------------------------|-----------------------------------------|
| `apiURL`      | WebSocket server URL                         | `https://nola-chat-dev3.responsum.ai`   |
| `apiPath`     | WebSocket path                               | `/ws-public/socket.io/`                 |
| `appID`       | Application ID for auth                      | `has`                                   |

### Metadata

Pass session-specific data:

```kotlin
val location: Map<String, Any> = mapOf("latitude" to "29.9902", "longitude" to "-95.3368")
val metadata = mapOf(
    "airport" to "HOU",
    "language" to "ja",
    "location" to location
)
```

### Other Options

| Parameter               | Type     | Description                                               | Default          |
|-------------------------|----------|-----------------------------------------------------------|------------------|
| `cleanOldHistory`       | Boolean  | Clears chat history on new session                        | `false`          |
| `speechToTextLanguage`  | String   | Language for speech-to-text (e.g. `"hr-HR"`)              | `en-US`          |
| `dateTimeFormat`        | String   | Format pattern used to display message timestamps (e.g. "M/d/yyyy, h:mm")        | `M/d/yyyy, h:mm` |


---

## Full Example

```kotlin
val location: Map<String, Any> = = mapOf("latitude" to "29.9902", "longitude" to "-95.3368")

ResChat.startChat(
    context = this,
    apiURL = "https://nola-chat-dev3.responsum.ai",
    apiPath = "/ws-public/socket.io/",
    appID = "has",
    metadata = mapOf(
        "airport" to "IAH",
        "language" to "en",
        "location" to location
    ),
    cleanOldHistory = true,
    speechToTextLanguage = "hr-HR",
    dateTimeFormat = "hh:mm - dd.MM.YYYY.",
    colorCustomization = ColorCustomization(
        chatBotAvatarBackgroundColor = Color.Black,
        userAvatarBackgroundColor = Color.Gray,
        backgroundColor = Color.DarkGray,
        botChatBubbleBackgroundColor = Color.Black,
        timestampTextColor = Color.LightGray,
        messageTextColor = Color.White,
        inputFieldPlaceholderTextColor = Color.White,
        inputFieldBorderColor = Color.Gray,
        botChatBubbleShadowColor = Color.White,
        sendIconColor = Color.White,
        textColor = Color.White,
        settingsStartChatBackgroundColor = Color.White,
        settingsStartChatTextColor = Color.Black,
        microphoneIconColor = Color.White
    ),
    imageCustomization = ImageCustomization(
        microphoneIcon = R.drawable.custom_mic_icon,
        sendIcon = R.drawable.custom_send_icon
    ),
    navigationBarCustomization = NavigationBarCustomization(
        title = "Custom Airport HelpBot",
        backgroundColor = Color.Gray,
        textColor = Color.White,
        backButtonColor = Color.White,
        font = TextStyle(
            fontSize = 18.sp,
            fontWeight = FontWeight.Bold
        ),
        backButtonImage = R.drawable.custom_back_button
    )
)
```

---

## Changelog

### v1.0.8
- Bug fixes and improvements

### v1.1.1
- Added time and date format configuration

---

Enjoy building with ResChat SDK!  
Feedback and contributions are welcome.
