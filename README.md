# Watchlist-project-info-only
Watchlist project info only, no code is included, just a description of the project i am working on and its features

# WatchList 🎬📺

A modern Android application for discovering, tracking, and managing your favourite movies and TV shows. Built with Jetpack Compose and following clean architecture principles.

[![Kotlin](https://img.shields.io/badge/Kotlin-1.9+-purple.svg)](https://kotlinlang.org)
[![Compose](https://img.shields.io/badge/Jetpack%20Compose-Latest-blue.svg)](https://developer.android.com/jetpack/compose)
[![API](https://img.shields.io/badge/API-24%2B-brightgreen.svg)](https://android-arsenal.com/api?level=24)

---

## ✨ Features

### 🏠 Home Feed
- **Now Playing Movies**: Browse current theatrical releases in a horizontal carousel — favourite directly from the home screen
- **TV Shows Airing Today**: Discover what's on TV right now — favourite without leaving the feed
- **Entertainment News**: Top Guardian articles in a hero + simple hybrid list
- **Persistent offline news**: Articles cached locally so the feed loads without a connection

---

### 🎥 Movie Discovery
- **Popular, Top Rated & Upcoming** carousels on the Movies tab
- **Genre filter chips** to narrow results by category
- **Region-aware upcoming** — "📍 Local" chip shows releases relevant to your country

### 📺 TV Show Discovery
- **Airing Today, Top Rated, On Air & Upcoming** carousels on the TV tab
- **Genre filter chips** + **Streaming network filter** — browse by Netflix, HBO, Disney+, Apple TV+, Amazon Prime, or Hulu

---

### 🎬 Detail Screens
Every Movie and TV Show detail screen includes:

- **Backdrop + poster header** with rating badge
- **Genre chips**, runtime, language, release date
- **Trailers row** — embedded YouTube player
- **Overview card** with expandable text
- **Box office figures** (movies) / **Season & episode stats** (TV)
- **Production companies**, cast & crew rows
- **Reviews link** — browse all TMDB reviews; full review detail screen with author and rating
- **Where to Watch** — streaming provider logos grouped into Stream / Rent / Buy, region-aware
- **Similar Movies / Similar TV Shows** — horizontal carousel of related titles with heart toggles
- **In the News** — up to 10 Guardian articles matching the title, cached locally for 24 hours
- **"Offline · Cached X ago"** banner when data is served from local cache

#### ✨ AI Features on Detail Screens
- **"Why should I watch this?"** — tap the button to get a 2–3 paragraph AI-written pitch tailored to that specific title (rating, genres, overview)
- **"📋 AI Review Summary"** — aggregates up to 10 cached user reviews into a structured verdict: one-sentence summary, top 3 things audiences love, top 3 criticisms, and who it's best for

---

### 🔍 Search
- **AI-Powered Search**: Describe what you want in natural language — "A thriller from the last 3 years with no violence" — and get curated results from TMDB
- **Title Search**: Find content by exact name
- **Dual search modes**: Switch between AI and traditional search seamlessly
- **Media type filtering**: Filter results by movies or TV shows
- **Optimistic favourite toggle** directly from search results

---

### 🤖 AI-Powered Discovery Screens

#### 😊 Mood Discovery
- Describe how you're feeling in plain text — "happy and excited", "want something dark and intense"
- The LLM analyses your mood and suggests a personalised mix of movies and TV shows
- Results are fetched from TMDB and marked with your existing favourites

#### 🌙 Watch Night Planner
- Configure your evening: audience type, optional theme, and how many films you want
- The LLM builds a curated playlist with a one-sentence reason for each pick
- Results link directly to each movie's detail screen

#### 💎 Hidden Gems
- Requires at least 3 saved favourites to activate
- The LLM analyses your taste from your top favourites and suggests 4 critically acclaimed but underappreciated films (rating > 7.0, under 50k votes)
- Each suggestion comes with a personalised reason matching your taste

---

### 📶 Offline Support
- **Full offline detail screens** — Movie and TV Show detail screens load from a local Room cache written during your last online visit
- **Coil 150 MB disk cache** keeps poster and backdrop images available without a network connection
- **"Offline · Cached X ago"** banner at the top of the screen when data is served from cache
- Cache is silently refreshed every time you visit a screen while online — no manual action needed

---

### ⭐ Favourites
- **Save favourites**: Mark your favourite movies and TV shows with a heart from any screen
- **Organised list**: Combined favourites screen with sort options — name, date added, rating
- **Persistent storage**: Saved locally in Room
- **Cloud sync**: Bidirectional sync with Firebase Firestore when signed in — favourites survive device changes

---

### 🔔 Release Alerts & Notifications
- **WorkManager background job** periodically checks for upcoming releases of your favourited media
- **Configurable timing**: Alert on the same day, 1 day before, or 1 week before release
- **Deep links**: Tapping a notification navigates directly to that movie or TV show's detail screen

---

### 📰 In the News (Detail Screens)
- Per-title Guardian news section on every Movie and TV Show detail screen
- Up to 10 articles fetched by title query with relevance filtering (excludes tangential mentions)
- Articles cached locally for 24 hours with a **"Cached X ago"** indicator
- Tapping an article opens the full news screen with HTML body and media carousels

---

### 📺 Where to Watch
- Streaming provider logos on every Movie and TV Show detail screen
- Grouped into **Stream**, **Rent**, and **Buy** sections
- Region-aware — uses your configured country code from Settings
- "Not available in your region" shown when no providers are found

---

### 👥 Cast & Crew
- **Cast row** on every detail screen with profile images and character names
- **Person detail screen**: biography, birthday, place of birth, known-for department, and full filmography across movies and TV

---

### ⚙️ Settings
- **Account**: Google Sign-In, sign-out, and manual Firestore sync with status indicator
- **Theme**: Light, Dark, or System — persisted via DataStore
- **Region**: Override your country code for localised discovery and Watch Providers
- **Hide Adult Content**: Toggle to filter out adult-rated results
- **Release Alerts**: Enable/disable notifications and choose timing preference
- **Export Favourites**: Save your entire favourites list to a JSON file
- **Import Favourites**: Restore from a previously exported JSON file
- **Clear Cache**: Purge non-favourite data (news, upcoming lists, reviews) while keeping your saved films

---

### 🎨 Modern UI/UX
- **Material Design 3** throughout — cards, chips, FABs, elevated surfaces, bottom sheets
- **Dark + Light themes** — fully themed with `tertiaryContainer`, `primaryContainer`, and `surfaceVariant` tokens
- **Smooth transitions** and content-size animations
- **Expandable text** for long overviews
- **Optimistic UI updates** — hearts toggle instantly, state syncs in the background

---

### 🔥 Firebase Integration
- **Crashlytics**: Automatic crash reporting and error tracking
- **Analytics**: User behaviour and app usage tracking
- **Firestore**: Cloud storage for favourites sync
- **Firebase Auth**: Google Sign-In
- **Abstracted behind interfaces** for full testability — `CrashReporter`, `FavouritesSyncRepository`

---

## 🏗️ Architecture

The app follows **Clean Architecture** principles with clear separation of concerns:

```
┌─────────────────────────────────────────────┐
│              Presentation Layer              │
│   (UI, ViewModels, Compose Screens)         │
├─────────────────────────────────────────────┤
│               Domain Layer                   │
│        (Use Cases, Entities)                 │
├─────────────────────────────────────────────┤
│                Data Layer                    │
│   (Repositories, Data Sources, Room DB)     │
└─────────────────────────────────────────────┘
```

### Key Components
- **UI Layer**: Jetpack Compose with state-based UI, `StateFlow` collected via `collectAsState()`
- **ViewModel**: Manages UI state with `MutableStateFlow`; sealed class states (Loading / Content / Error)
- **Use Cases**: Single-responsibility, all return `Result<T>` — no exceptions escape the domain layer
- **Repository**: Abstracts data sources; offline-aware (cache-write on success, cache-read on failure)
- **Data Sources**: Remote (Retrofit) and Local (Room database)

---

## 🛠️ Tech Stack

### Core
- **Kotlin** — Primary language
- **Jetpack Compose** — Declarative UI
- **Material Design 3** — UI design system

### Architecture Components
- **ViewModel** — Lifecycle-aware state management
- **Room 2.8.3** — Local database — 10 entities across 3 schema migrations (v5 → v6 → v7)
- **Hilt** — Dependency injection
- **DataStore Preferences** — Lightweight settings persistence (theme, region, alert prefs)
- **WorkManager** — Background release-check job
- **Compose Destinations** — Type-safe navigation with deep link support

### Networking
- **Retrofit** — REST API client
- **Gson** — JSON serialization / deserialization
- **OkHttp** — HTTP client with header interceptors for auth tokens

### Image Loading
- **Coil 2.7.0** — Image loading optimised for Compose; **150 MB disk cache** for offline support

### APIs
| API | Used for |
|---|---|
| **TMDB** | Movies, TV shows, cast, trailers, watch providers, search |
| **The Guardian** | Entertainment news (home feed + per-title detail sections) |
| **OpenAI** | Alternative LLM backend (`gpt-4o-mini`) |
| **Anthropic** | Current LLM backend (`claude-haiku-4-5`) |

### Firebase
- **Firebase Auth** — Google Sign-In
- **Firebase Firestore** — Cloud favourites sync
- **Firebase Crashlytics** — Crash reporting
- **Firebase Analytics** — Usage tracking
- **Firebase BOM** — Centralised version management

### Testing
- **JUnit 4** — Unit testing framework
- **MockK** — Kotlin-first mocking library
- **Coroutines Test** — `runTest`, `advanceUntilIdle` for coroutine/flow testing
- **AppTestRule** — Custom rule combining `MockKRule` and a `TestCoroutineDispatcher`

---

## 🤖 AI / LLM Architecture

All AI features are routed through a single `AiTextClient` interface (`data/datasource/ai/`). No use case, repository, or ViewModel knows which LLM provider is active — swapping the backend is a one-line change in the DI module.

```kotlin
// data/datasource/ai/AiTextClient.kt
interface AiTextClient {
    suspend fun complete(prompt: String): Result<String>
}
```

### Switching providers

Change **one line** in `di/SearchSuggestionModule.kt`:

```kotlin
// Use OpenAI (gpt-4o-mini)
fun provideAiTextClient(client: OpenAiTextClient): AiTextClient = client

// Use Anthropic (Claude) ← current
fun provideAiTextClient(client: AnthropicTextClient): AiTextClient = client
```

### Current provider

**Anthropic** — model `claude-haiku-4-5` (fastest / cheapest tier).
Change the model constant in `data/model/anthropic/AnthropicRequest.kt`:

| Model | Speed | Cost |
|---|---|---|
| `claude-haiku-4-5` | Fastest | Cheapest ✅ current |
| `claude-sonnet-4-5` | Balanced | Mid |
| `claude-opus-4-5` | Best quality | Most expensive |

Full model list: https://docs.anthropic.com/en/docs/about-claude/models/overview

### Features powered by AI

| Feature | Prompt style | Output |
|---|---|---|
| AI Search | Natural-language query → structured TMDB searches | Movie/TV list |
| Mood Discovery | Free-text mood → `[Title]` / `[TV: Title]` tokens | Movie + TV mix |
| Watch Night Planner | Audience + theme + count → `[Title]: reason` lines | Curated playlist |
| Hidden Gems | Top 5 favourites → `[Title]: reason` lines | 4 obscure picks |
| "Why should I watch this?" | Title + rating + genres + overview → prose | 2–3 paragraph pitch |
| AI Review Summary | Up to 10 cached reviews → JSON | Structured verdict |

---

## 🗄️ Room Database

**Version 7** — 10 entities across 3 migrations:

| Table | Purpose |
|---|---|
| `favourite_movies` | Saved favourite movies |
| `favourite_tv_shows` | Saved favourite TV shows |
| `NewsArticles` | Home-screen Guardian news cache |
| `media_news_articles` | Per-title Guardian news cache (detail screens) |
| `movie_reviews` | TMDB movie review cache |
| `tv_show_reviews` | TMDB TV show review cache |
| `upcoming_movies` | Upcoming movie cache (region-aware) |
| `upcoming_tv_shows` | Upcoming TV show cache |
| `cached_movie_details` | Full offline movie detail cache |
| `cached_tv_show_details` | Full offline TV show detail cache |

---

## 📋 Prerequisites

Before you begin, ensure you have:
- Android Studio Hedgehog or later
- JDK 8 or higher
- Android SDK with minimum API level 24

## 🔑 API Keys Setup

This app requires API keys from four services:

1. **TMDB API** — [https://www.themoviedb.org/](https://www.themoviedb.org/)
2. **The Guardian API** — [https://open-platform.theguardian.com/](https://open-platform.theguardian.com/)
3. **OpenAI API** — [https://platform.openai.com/](https://platform.openai.com/) *(optional — only needed if switching the AI backend)*
4. **Anthropic API** — [https://console.anthropic.com/](https://console.anthropic.com/)

Keys are read from environment variables at Gradle build time and compiled into `BuildConfig`. They are never committed to source control.

| `BuildConfig` field | Env var name | Service |
|---|---|---|
| `API_TOKEN` | `API_TOKEN` | TMDB |
| `API_TOKEN_GUARDIAN` | `API_TOKEN_GUARDIAN` | The Guardian |
| `API_TOKEN_OPEN_API` | `API_TOKEN_OPEN_API` | OpenAI |
| `API_TOKEN_ANTHROPIC` | `API_TOKEN_ANTHROPIC` | Anthropic |

### Environment Variables — macOS (important)

> ⚠️ **Do not rely on `~/.zshrc` alone for Android Studio builds.**
>
> macOS GUI apps launched from the Dock or Spotlight do **not** source shell profile files. They inherit environment from **launchd** only. Adding keys to `~/.zshrc` makes them visible in terminal builds but not in Android Studio's Gradle process.

#### Permanent fix — launchd user agent plist

Create `~/Library/LaunchAgents/com.user.environment.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.user.environment</string>
    <key>ProgramArguments</key>
    <array>
        <string>sh</string>
        <string>-c</string>
        <string>
            launchctl setenv API_TOKEN your_tmdb_token
            launchctl setenv API_TOKEN_GUARDIAN your_guardian_token
            launchctl setenv API_TOKEN_OPEN_API your_openai_token
            launchctl setenv API_TOKEN_ANTHROPIC your_anthropic_token
        </string>
    </array>
    <key>RunAtLoad</key>
    <true/>
</dict>
</plist>
```

Load it immediately (no restart needed):
```bash
launchctl load ~/Library/LaunchAgents/com.user.environment.plist
```

#### Adding a new API key in future

1. Add a `launchctl setenv NEW_KEY value` line to the plist above
2. Reload it:
   ```bash
   launchctl unload ~/Library/LaunchAgents/com.user.environment.plist
   launchctl load ~/Library/LaunchAgents/com.user.environment.plist
   ```
3. Kill the Gradle daemon and relaunch Android Studio:
   ```bash
   ./gradlew --stop
   open -a "Android Studio"
   ```

> The Gradle daemon is a long-lived JVM process (stays alive ~3 hours) with a frozen environment. Even restarting Android Studio doesn't kill it — use `./gradlew --stop` after adding a key for the first time.

#### For Windows

```cmd
setx API_TOKEN "your_tmdb_api_token"
setx API_TOKEN_GUARDIAN "your_guardian_api_token"
setx API_TOKEN_OPEN_API "your_openai_api_token"
setx API_TOKEN_ANTHROPIC "your_anthropic_api_token"
```

---

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/MovieListPractise.git
   cd MovieListPractise
   ```

2. **Set up API keys** (see above)

3. **Set up Firebase**
   - Follow the detailed guide at [docs/firebase-setup.md](docs/firebase-setup.md)
   - Create a Firebase project at [https://console.firebase.google.com/](https://console.firebase.google.com/)
   - Download `google-services.json` and replace `app/google-services.json`
   - Enable Crashlytics, Analytics, Auth, and Firestore in Firebase Console

4. **Open in Android Studio**, sync Gradle, build, and run

---

## 🧪 Testing

```bash
# All unit tests
./gradlew testDebugUnitTest

# Single test class
./gradlew testDebugUnitTest --tests "com.jonathan.watchlist.data.datasource.news.MediaNewsRepositoryImplTest"

# Instrumented tests
./gradlew connectedAndroidTest
```

Test coverage includes:
- Repository cache-hit / cache-miss branches (`MovieRepositoryImplTest`, `MediaNewsRepositoryImplTest`)
- All AI use cases via mocked `AiTextClient` (no network calls in tests)
- ViewModel state transitions (`MovieDetailsViewModelTest`, `TopMoviesViewModelTest`, …)
- Guardian news relevance filtering and phrase-query encoding

---

## 📱 App Structure

```
app/src/main/kotlin/com/jonathan/
├── watchlist/
│   ├── data/
│   │   ├── dao/               # Room DAOs (favourite, review, upcoming, cache, news)
│   │   ├── datasource/        # API services + repository impls
│   │   │   ├── ai/            # AiTextClient interface + OpenAI / Anthropic impls
│   │   │   ├── api/           # Retrofit services (TMDB, Guardian, OpenAI)
│   │   │   ├── movies/        # Movie data source + repository
│   │   │   ├── news/          # News + media-news repositories
│   │   │   └── tvshow/        # TV show data source + repository
│   │   └── model/             # Data models (movies, TV, news, person, review, …)
│   ├── di/                    # Hilt modules
│   ├── home/                  # Home screen (now playing, airing today, news feed)
│   ├── movie/                 # Movies tab + detail screen + domain use cases
│   ├── tv/                    # TV tab + detail screen + domain use cases
│   ├── search/                # Unified search (AI + title)
│   ├── mood/                  # Mood Discovery screen
│   ├── watchnight/            # Watch Night Planner screen
│   ├── suggestion/            # Hidden Gems screen
│   ├── favourites/            # Favourites list
│   ├── review/                # Review list + detail
│   ├── person/                # Person / cast detail
│   ├── news/                  # News article screen
│   ├── settings/              # Settings screen + sync / export / import
│   ├── notifications/         # WorkManager release-check worker + NotificationHelper
│   └── ui/                    # Shared composables, theme, navigation
└── crashlytics/               # CrashReporter interface + Firebase implementation
```

---

## 🤝 Contributing

Contributions are welcome! Please open an issue first for major changes, then:

1. Fork the project
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 👨‍💻 Author

**Jonathan**

## 🙏 Acknowledgments

- [TMDB](https://www.themoviedb.org/) for movie and TV data
- [The Guardian](https://www.theguardian.com/) for entertainment news
- [Anthropic](https://www.anthropic.com/) for Claude AI
- [OpenAI](https://openai.com/) for GPT AI
- All open-source libraries used in this project

---

⭐ If you find this project useful, please consider giving it a star on GitHub!

