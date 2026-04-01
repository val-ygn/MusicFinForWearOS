# JellyfinForWearOS 
## The development of the app is paused right now, more info on the website.
**(In Development, it may change)**
**Informations can be changed on the Website (currently in French), so check it out (pinned on the sidebar)**

Please note that this description is in 2 Parts.
The app is not yet ready to be launched. I am actually working on it.

## PART 1: Key Information (General Public)
This section is designed to present the project in a clear and accessible way for everyone.

### 1.1 Introduction to the Concept
Jellyfin for WearOS is an innovative solution for Jellyfin media server users who own a WearOS smartwatch (version 3.0 and above). Today, our watches have become independent companions. The goal of this app is to free users from the need to carry their smartphones while enjoying their personal library of music and audiobooks.

### 1.2 Key Features
The app does more than just stream audio; it offers a complete experience tailored for the wrist:

Total Freedom (Streaming & Offline): Whether you are connected to your home Wi-Fi or in the middle of a forest without a signal, your music remains accessible. The "Download" mode allows you to store your favorite tracks directly in the watch's memory.

Audiobook Specialization: Unlike standard music players, this app remembers exactly where you left off in your audiobook, allowing you to resume listening instantly.

Simplified Ecosystem: Thanks to the smartphone companion app, the initial setup—which is often a hassle on a watch (typing URLs, passwords)—becomes child's play.

### 1.3 Daily User Experience
Imagine your routine:

Morning: You open the app on your watch. With a quick glance at the "Tile" on your watch face, you can see your recommended albums.

During Exercise: You leave your phone at home. Your Bluetooth headphones are connected directly to your watch. You launch your "Running" playlist, downloaded the night before.

Evening: You pick up your audiobook where you left off. With a simple gesture on the screen, you can skip back 30 seconds to replay an important passage.

### 1.4 Why is this app necessary?
Currently, there are very few high-quality options for accessing a Jellyfin server on WearOS. This project fills a technological gap by offering a modern, dark interface (to save battery on OLED screens) that is intuitive, respects Jellyfin’s visual identity, and is fully optimized for small circular displays.

## PART 2: Detailed Information (Technical)
This section details the technological choices and the internal architecture for the development.

### 2.1 Software Architecture and Environment
Development is based on the latest standards of the Android Wearable ecosystem:

Operating System: Minimum WearOS 3.0 (API 30+).

Language: Kotlin, chosen for its safety and conciseness.

Graphical Interface: Jetpack Compose for Wear OS. This framework allows for the creation of reactive interfaces that adapt perfectly to round screens thanks to components like ScalingLazyColumn.

Audio Management: The implementation of Media3 with ExoPlayer ensures compatibility with numerous formats (MP3, FLAC, OGG, OPUS) and smooth handling of adaptive streaming.

### 2.2 Configuration and Pairing System (Onboarding)
The major challenge is authentication. We use two methods:

Proximity Communication: The Wearable Data Layer API allows for message exchange between the phone and the watch. The phone, already connected to the Jellyfin server, securely transmits the server address and the Access Token.

Token System (Fallback): If the Bluetooth link fails, the watch generates a unique 6-digit code. The user enters this code into the smartphone app to validate pairing via Jellyfin’s discovery services.

### 2.3 Advanced Media and Storage Management
Data Persistence: A local Room database stores metadata for downloaded files (titles, artists, file paths, playback progress).

Caching Strategy: For streaming, a circular cache is used to preload the next few minutes of audio, preventing micro-stutters during transitions between Wi-Fi or 4G antennas.

Storage Optimization: Users can set a storage limit (e.g., 2 GB). The app offers "smart cleaning," prioritizing the deletion of files already listened to (especially for audiobooks).

### 2.4 Navigation and System Integration
The interface is structured in several layers for optimal execution speed:

Hierarchical Navigation: Home > Library > Artist > Album > Player.

Touch Interaction: Use of swipe gestures to toggle between the tracklist and the playback control menu.

Hardware Support: Integration of the Rotary Input (rotating crown) for smooth scrolling and precise volume control.

Tiles: Developed with the Tiles API, these allow users to launch actions without opening the full app, reducing CPU consumption.

### 2.5 Development Challenges to Address
Power Saving: Limiting CPU wakeups during downloads. Using WorkManager to schedule heavy tasks while the device is charging.

Bluetooth Management: Ensuring stable and automatic reconnection of headphones without interrupting playback. Managing audio priorities to avoid saturating Bluetooth bandwidth.

Synchronization: Updating playback progress on the Jellyfin server as soon as the watch regains an internet connection, while handling version conflicts if the media was played on another device in the meantime.
