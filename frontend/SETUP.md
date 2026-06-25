# Frontend Setup Guide - Angular 18

## Prerequisites
- Node.js 18+ (Download from https://nodejs.org/)
- Angular CLI 18+
- npm or yarn package manager

## Project Structure
```
frontend/
├── user-app/              # User Calendar Interface
├── admin-dashboard/       # Admin Panel
├── shared/               # Shared components & services
└── SETUP.md
```

## Step 1: Install Angular CLI

```bash
npm install -g @angular/cli@18
ng version
```

## Step 2: Create User App

```bash
cd frontend
ng new user-app --routing --style=css
cd user-app
```

## Step 3: Create Admin Dashboard

```bash
cd ../
ng new admin-dashboard --routing --style=css
cd admin-dashboard
```

## Step 4: Install Dependencies

### For User App
```bash
cd user-app
npm install
npm install @angular/material @angular/cdk
npm install @ngx-translate/core @ngx-translate/http-loader
npm install @ngrx/store @ngrx/effects @ngrx/store-devtools
npm install primeng primeicons
npm install axios
npm install date-fns
```

### For Admin Dashboard
```bash
cd ../admin-dashboard
npm install
npm install @angular/material @angular/cdk
npm install @ngx-translate/core @ngx-translate/http-loader
npm install @ngrx/store @ngrx/effects @ngrx/store-devtools
npm install primeng primeicons
npm install axios
npm install date-fns
```

## Step 5: Configure i18n (Internationalization)

### User App
```bash
cd user-app
ng add @ngx-translate/core
```

Create translation files:
```
src/assets/i18n/
├── en.json        # English
├── hi.json        # Hindi
├── te.json        # Telugu
├── ta.json        # Tamil
├── kn.json        # Kannada
└── ml.json        # Malayalam
```

## Step 6: Run Development Server

### User App
```bash
cd user-app
ng serve
# Open http://localhost:4200
```

### Admin Dashboard
```bash
cd ../admin-dashboard
ng serve --port 4201
# Open http://localhost:4201
```

## Step 7: Build for Production

### User App
```bash
cd user-app
ng build --configuration production
```

### Admin Dashboard
```bash
cd ../admin-dashboard
ng build --configuration production
```

## Folder Structure

```
user-app/src/
├── app/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── interceptors/
│   ├── models/
│   ├── app.config.ts
│   ├── app.component.ts
│   └── app.routes.ts
├── assets/
│   └── i18n/
├── environments/
├── index.html
├── main.ts
└── styles.css
```

## Next Steps
1. Create authentication services
2. Build calendar components
3. Implement event management
4. Add festival management
5. Setup state management
