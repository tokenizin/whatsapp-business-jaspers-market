# Env & token reference

Map from **Access Token Info** (Meta token debugger) to this app.

| Token debugger field | Use in this project |
|----------------------|----------------------|
| **App ID** | `APP_ID` in `.env` (and in `template.sh` as `APPID`). Example: `698713283268623` (Prestix.vip - Test1). |
| **Access token (the actual string)** | `ACCESS_TOKEN` in `.env`. Used by `services/graph-api.js` for all WhatsApp API calls. |
| **Granular scope object for whatsapp_business_*** | That ID is your **WABA ID** (WhatsApp Business Account). Put it in `.env` as `WABA_ID` and in `template.sh` as `WABAID`. Example: `1324961076109950`. |

## Token type

- **User token** (like the one you debugged): Long‑lived user token; fine for development. Put it in `ACCESS_TOKEN`.
- **System user token**: Preferred for production (no user session). Create in Meta Business Suite → Business Settings → Users → System users → Generate token; use that value for `ACCESS_TOKEN`.

## Scopes used by this app

Your token should include at least:

- `whatsapp_business_messaging`
- `whatsapp_business_management`
- `whatsapp_business_manage_events`

Optional for templates / assets: `pages_show_list`, `business_management` (for the WABA).

## Single source of truth

- **Runtime** (`app.js`): reads `ACCESS_TOKEN`, `APP_SECRET`, `VERIFY_TOKEN`, `REDIS_*` from `services/config.js` (from `.env`). `APP_ID` is not used by the Node app at runtime.
- **Templates** (`template.sh`): set `APPID` and `WABAID` in the script (or export from `.env`) so they match `APP_ID` and `WABA_ID`.

Keep `APP_ID` and `WABA_ID` in `.env` and, if you run `template.sh`, sync them into the script or source `.env` before running.
