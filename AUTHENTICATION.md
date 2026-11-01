# Minecraft API access request

## Application

- Name: **Moss Launcher**
- Maintainer: **Whilechocolate**
- Client ID: `38d0dbb0-e88b-4756-879d-e05322698703`
- Windows public/native client, personal Microsoft accounts
- OAuth authorization code with PKCE through the system browser
- Loopback redirect: `http://localhost` with a dynamically assigned port
- Requested Microsoft scopes: `XboxLive.signin`, `offline_access`
- No embedded client secret

## Intended service calls

| Service | Purpose |
| --- | --- |
| Microsoft identity platform | Authorization discovery, browser authorization and token exchange/refresh |
| `user.auth.xboxlive.com/user/authenticate` | Obtain an Xbox user token from the Microsoft credential |
| `xsts.auth.xboxlive.com/xsts/authorize` | Obtain an XSTS token for `rp://api.minecraftservices.com/` |
| `api.minecraftservices.com/authentication/login_with_xbox` | Exchange the verified Xbox identity for a Minecraft session |
| `api.minecraftservices.com/entitlements/mcstore` | Check Java Edition entitlement information |
| `api.minecraftservices.com/minecraft/profile` | Retrieve the player's Minecraft profile and UUID |

The launcher returns a verified Minecraft identity only after the profile and entitlement checks succeed. Each player uses their own account. Source downloads and appearance customization are separate from account authentication.

## Current status

On 1 November 2026, the maintainer supplied an AppID review approval notification and confirmed successful Microsoft/Minecraft authentication, Minecraft game launch, and resource installation. The earlier HTTP 403 application-registration block is resolved for this client ID. This records the maintainer's successful user test; it does not imply every Minecraft release, loader or mod combination has been tested.

The launcher displays the failing service stage and sanitized status information. Browser completion alone is not treated as Minecraft authentication success. Signing in is never replaced by another launcher's application ID.

## Review contact

The maintainer's contact email and tenant ID are supplied privately in the review form. A reviewer may use that email to request additional application information. No account passwords, OAuth codes, Xbox/XSTS tokens, Minecraft bearer tokens, private API keys, or encrypted credential caches are published here.
