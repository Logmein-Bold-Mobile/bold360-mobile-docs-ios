---
layout: default
title: User Input Field
parent: UI Customization
grand_parent: Chat Configuration 
# permalink: /docs/chat-configuration/ui-customization/user-input-field
nav_order: 2
---

# User Input Field {{site.data.vars.force-work}}
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

- TOC
{:toc}

---

## Overview
Usually appears at the bottom of the chat screen. Contains the users typed/recorded message, until it was sent.   
The behavior and functionality of the input field is defined by the active chat type.   
{: .overview}

> e.g., The **upload icon** will appear only on live chats and only if was enabled by configuration.

## Available features
- Typing and sending messages 
- [Autocomplete](~/docs/advanced-topics/autocomplete/in-chat)
- [Voice recording and readout control](~/docs/advanced-topics/voice)
- [File upload](~/docs/advanced-topics/file-upload) on live chats

---
## UI customization
- ### Configuration   
  The SDK provides a configurable _user input field_ implementation.
  The default configuration can be changed via `ChatController.viewConfiguration.searchViewConfig` 
  
  ```swift
  let searchViewConfig = chatController.viewConfiguration.searchViewConfig
  searchViewConfig.backgroundColor = ...
  searchViewConfig.textColor = ...
  searchViewConfig.customFont = ...
  searchViewConfig.sendIcon = ...
  searchViewConfig.uploadIcon = ...
  // Border Configuration
  searchViewConfig.border.color = ...
  searchViewConfig.border.width = ...
  searchViewConfig.border.cornerRadius = ...
  // Voice Support Features
  searchViewConfig.voiceEnabled = // defines whether or not to enable recording
  searchViewConfig.speechOnIcon = ...
  searchViewConfig.speechOffIcon = ...
  searchViewConfig.readoutIcon = ...
  //  Specifies the BCP-47 language tag representing the language for voice recognition.
  /// Examples: en-US (U.S. English), fr-CA (French Canadian)
  searchViewConfig.languageCode = "en-US" 
  ```

  |![]({{'/assets/images/searchview.png' | relative_url}}){: .image-70}|![]({{'/assets/images/placeholder.png' | relative_url}}){: .image-70}|![]({{'/assets/images/autocomplete.png' | relative_url}}){: .image-70}
  |---|---|---|
  |![]({{'/assets/images/fileupload.png' | relative_url}}){: .image-70}|![]({{'/assets/images/recording.png' | relative_url}}){: .image-70}|![]({{'/assets/images/readout.png' | relative_url}}){: .image-70}
{: .mb-8}

---
## Hint configuration

- Hint configuration for AI chats is done on the [bold360ai console]({{'/assets/images/ai-hint-config.png' | relative_url}}).
  > Escalated chats will not effect the AI configured hint.

- Hint configuration for Live chats is done on the [bold admin console]({{'/assets/images/live-hint-config.png' | relative_url}}). 

- Hint configurations should be set by ChatController.ChatConfiguration.SearchViewConfiguration.PlaceholderConfiguration
  This resource will be used, if none of the above was provided, to the current active chat.

### Setting The PlaceholderConfiguration
  ```swift
  let placeholderConfiguration = PlaceholderConfiguration()
  placeholderConfiguration.readoutext = "Reading out.."
  placeholderConfiguration.recordText = "Recording now.."
  placeholderConfiguration.text = "Write here.."
  placeholderConfiguration.backgroundColor = UIColor.blue
  placeholderConfiguration.textColor = UIColor.red
  let customFont:CustomFont = CustomFont()
  customFont.font = UIFont.italicSystemFont(ofSize: 30)
  placeholderConfiguration.customFont = customFont
  searchViewConfig.placeholderConfiguration = placeholderConfiguration
  ```
---
## Known Issues
1. The ability to change the text inside the input field exists but does nothing:
```swift
chatController.viewConfiguration.searchViewConfig.text = "Does nothing"
```

  