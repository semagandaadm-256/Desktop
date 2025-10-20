# Pharmacy POS Offline Demo

This is a small demo WinForms application (C# /.NET) that shows an offline-capable cash-only pharmacy POS with a local SQLite store and a simple Sync button to push unsynced sales to a configurable server URL.

What it includes
- WinForms app (UI created in code) for simplicity.
- Local SQLite DB stored in AppData\Local\PharmacyPos\store.db
- Dapper for lightweight data access
- A SyncEngine that POSTs unsynced sales to a configurable /api/sync/push endpoint (mock mode available)
- GitHub Actions workflow that builds a self-contained single-file Windows EXE and uploads it as an artifact

How to build locally
1. Install .NET 7 SDK (or later) and Visual Studio (or use dotnet CLI).
2. From repository root run:
   dotnet restore
   dotnet publish PharmacyPos/PharmacyPos.csproj -c Release -r win-x64 --self-contained true /p:PublishSingleFile=true /p:PublishTrimmed=true -o ./publish
3. The produced executable will be in `publish\` folder (PharmacyPos.exe).

How to use the demo
- Run the EXE. Click "Add product" to add a product to local DB (name, code, price).
- Click "New sale" to create a cash sale (select product and quantity).
- Click "Sync" to post unsynced sales to the server configured in `PharmacyPos/appsettings.json`.

Configuration
- Edit `PharmacyPos/appsettings.json` and set `ServerUrl` to your server's base URL (for testing you can use a mock server). The app uses `MockMode: true` by default so Sync simulates success.

Notes
- This is a small demo to get you started. It does not implement full auditing, encryption of tokens, or advanced conflict resolution; add those before production use.