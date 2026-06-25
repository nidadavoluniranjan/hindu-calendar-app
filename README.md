# Hindu Calendar Application

A comprehensive multi-platform Hindu calendar application featuring Gregorian and Lunar calendar synchronization, festivals, auspicious dates (Panchang), and event management.

## 🌐 Platforms Supported

- **Mobile:** Flutter (iOS & Android)
- **Web:** Angular (User Interface + Admin Dashboard)
- **Backend:** ASP.NET Core Web API with PostgreSQL

## 🎯 Features

### Core Features
- ✅ Hindu Calendar (Gregorian + Lunar Calendar Sync)
- ✅ Festivals & Auspicious Dates (Muhurat, Panchang)
- ✅ Events & Reminders Management
- ✅ Admin Panel for Festival Management
- ✅ User Authentication (JWT)
- ✅ Multi-language Support (Hindi, Telugu, Tamil, Kannada, Malayalam)

### Languages Supported
- 🇮🇳 Hindi (हिन्दी)
- 🇮🇳 Telugu (తెలుగు)
- 🇮🇳 Tamil (தமிழ்)
- 🇮🇳 Kannada (ಕನ್ನಡ)
- 🇮🇳 Malayalam (മലയാളം)

## 📁 Project Structure

```
hindu-calendar-app/
├── backend/                    # ASP.NET Core Web API
│   ├── HinduCalendar.API/
│   ├── HinduCalendar.Core/
│   ├── HinduCalendar.Infrastructure/
│   └── HinduCalendar.sln
├── frontend/                   # Angular Web Application
│   ├── user-app/              # User Interface
│   ├── admin-dashboard/       # Admin Panel
│   └── shared/                # Shared components & services
├── mobile/                     # Flutter Application
│   └── hindu_calendar_flutter/
├── docs/                       # Documentation
└── README.md
```

## 🛠 Tech Stack

### Backend
- **Framework:** ASP.NET Core 8.0+
- **Database:** PostgreSQL
- **ORM:** Entity Framework Core
- **Authentication:** JWT (JSON Web Tokens)
- **API:** RESTful API

### Frontend (Web)
- **Framework:** Angular 18+
- **UI Library:** Angular Material / Prime NG
- **State Management:** NgRx / Akita
- **Localization:** ngx-translate

### Mobile (Flutter)
- **Framework:** Flutter 3.0+
- **State Management:** Provider / Riverpod
- **Local Storage:** Hive / SharedPreferences
- **Localization:** intl / Easy Localization

## 📦 Panchang & Calendar Integration

### Libraries Used
- **Astronomical Calculations:** Ephem / Python Astro Library
- **Hindu Calendar Conversion:** Drikpanchang or custom implementation
- **Festival Database:** Manual curated data + REST API

## 🔐 Authentication

- JWT Token-based authentication
- Refresh token mechanism
- Role-based access control (User, Admin)
- Secure password hashing

## 🚀 Getting Started

### Prerequisites
- .NET 8.0 SDK
- Node.js 18+
- Angular CLI
- Flutter SDK
- PostgreSQL

### Backend Setup
```bash
cd backend
dotnet restore
dotnet build
dotnet ef database update
dotnet run
```

### Frontend (Angular) Setup
```bash
cd frontend/user-app
npm install
ng serve
```

### Admin Dashboard Setup
```bash
cd frontend/admin-dashboard
npm install
ng serve --port 4201
```

### Flutter Mobile Setup
```bash
cd mobile/hindu_calendar_flutter
flutter pub get
flutter run
```

## 📚 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/refresh` - Refresh token

### Calendar
- `GET /api/calendar/month` - Get calendar for month
- `GET /api/calendar/festivals` - Get festivals for date range
- `GET /api/calendar/panchang/:date` - Get Panchang details

### Events
- `GET /api/events` - List user events
- `POST /api/events` - Create event
- `PUT /api/events/:id` - Update event
- `DELETE /api/events/:id` - Delete event

### Admin
- `GET /api/admin/festivals` - List all festivals
- `POST /api/admin/festivals` - Create festival
- `PUT /api/admin/festivals/:id` - Update festival
- `DELETE /api/admin/festivals/:id` - Delete festival

## 🌍 Localization

All UI text is localized to 5 languages with local touch. Language selection is available in:
- Mobile app settings
- Web user preferences
- Admin panel

## 📋 Database Schema

### Tables
- `Users` - User accounts
- `Festivals` - Hindu festivals
- `PanchangData` - Auspicious dates & timings
- `Events` - User events
- `Reminders` - Event reminders
- `Localization` - Multi-language content

## 🔄 Development Workflow

1. Create feature branch from `develop`
2. Make changes across backend/frontend as needed
3. Run tests locally
4. Create Pull Request
5. Code review
6. Merge to `develop`, then `main`

## 📝 License

[Choose your license - MIT, Apache 2.0, etc.]

## 👥 Contributors

- Lead Developer: nidadavoluniranjan

## 📧 Contact & Support

For issues, questions, or contributions, please create an issue in this repository.

---

**Last Updated:** June 2026
