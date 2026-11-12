# Japanese Learning Hub — Cloud Sync build

Static HTML/CSS/JavaScript app for GitHub Pages. Local learning data remains in LocalStorage and can additionally sync through the deployed Supabase Edge Function `jlh-sync`.

## Update GitHub Pages

Replace the existing repository-root files with these four files:
- `index.html`
- `styles.css`
- `app.js`
- `README.md`

Commit and push. No build step is required.

## First device (the laptop that already ran `create` in Supabase)

1. Open the app on the laptop and go to **Settings → Cloud Sync**.
2. Enter the deployed Edge Function URL. The default is `https://vtxsyhkweibykeyjhjka.supabase.co/functions/v1/jlh-sync`.
3. Enter the project's **Publishable key** (Supabase Dashboard → Project Settings → API Keys; use the publishable key, not a secret/service-role key).
4. Paste `workspaceId` from the successful `create` response into **Workspace ID**.
5. Paste `deviceToken` from that same `create` response into **Device Token**. Keep it private.
6. Click **Lưu cấu hình**, then **Upload dữ liệu máy này**. This uploads the laptop's current LocalStorage data to the workspace created with an empty `{}` payload.

Do not run `create` again for this workspace. It creates a separate workspace and a separate token.

## Pair a phone / second device

1. On the laptop, open Settings → Cloud Sync and click **Tạo mã ghép đôi**.
2. On the phone, open the same GitHub Pages app. In Settings → Cloud Sync, enter the same Function URL and Publishable key.
3. Enter the 12-character one-time pairing code and a device name, then click **Pair thiết bị này**.
4. If the cloud already contains data, confirm replacing the phone's local workspace with the cloud copy.

Pairing codes expire after 10 minutes and can only be used once. Generate a new one if it expires.

## Sync behavior

- Local changes are saved immediately to LocalStorage.
- Once a device is connected, changes are pushed to Supabase after a short debounce.
- Use **Pull dữ liệu Cloud** to explicitly replace this browser's local data with the cloud copy. The app asks for confirmation first.
- Revision conflicts pause automatic pushing to avoid silently overwriting newer cloud data. Pull the latest data and resolve the situation before continuing.
- Device credentials are stored in a separate browser LocalStorage key and are not included in the learning-data JSON backup.

## Security notes

- Never publish or share a device token, Supabase secret key, or service-role key.
- The browser only needs the Supabase Publishable key plus its own device token.
- The Edge Function must have JWT verification disabled if it is using the custom `x-jlh-device-token` authentication implemented in the function code.
- The Edge Function's allowed CORS origin must exactly match the deployed GitHub Pages origin.

## Existing dictionary limitation

This build does not bundle the complete JMdict or KANJIDIC2 datasets. It retains the existing starter entries and dictionary JSON import feature.
