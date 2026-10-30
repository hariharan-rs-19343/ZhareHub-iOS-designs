# ZhareHub — Mobile App Designs

Hi-fi iOS / iPadOS 26 designs for the ZhareHub app, built on the bound **ZhareHub Design System** (`_ds/zharehub-design-system-d00ac0e8-…`). Every screen ships in iPhone (portrait) and iPad (landscape), Light and Dark.

## Open this first

`ZhareHub Login.dc.html` — the canvas. One labelled row per screen, each row showing iPhone Light/Dark and iPad Light/Dark frames. Pan and zoom freely.

## Files

| File | Screen |
|---|---|
| `ZhareHub Login.dc.html` | Canvas holding every frame |
| `LoginScreen.dc.html` | Login: Zoho / Apple / Google sign-in |
| `AuthOverlay.dc.html` | Sign-in popups and flows shown over Login |
| `NoOrgScreen.dc.html` | Empty state when the user belongs to no organization |
| `AppListScreen.dc.html` | Application list grouped by date, with context menus |
| `AppDetailScreen.dc.html` | Application detail, Shared-with sheet, Share sheet |
| `SettingsScreen.dc.html` | Settings: profile, upgrade, orgs, teams, appearance, legal |
| `support.js` | Runtime (generated, don't edit) |

Every screen accepts `device` (`iPhone` / `iPad`) and `appearance` (`Light` / `Dark`). These are also exposed in the Tweaks panel.

## Screens

**Login**: sign-in options, plus popups for each flow.

**No Organization**: illustration, explanation and next action for users who aren't in an organization yet.

**Application List**: 38 apps split into Today, Yesterday, This Week, This Month and This Year. Scrollable. Long-press opens a context menu with Share and Delete.

**Application List: Loading**: skeleton cards that match the real card layout, pulsing while data loads (`loading` prop). Retry on an error screen shows this state, then the list.

**Application List: Errors**: Network, Fetch failed, OAuth token and Unknown (`error` prop). Each has an illustration, a title, a two-line message and Retry and/or Log Out.

**Search**: searches application names in the current tab (My Application or Shared with me), live as you type, keeping the date groups and full cards. States: results, loading (skeleton) and no results. On iPhone the glass search button expands into a bottom search field, and the Applications button exits search. On iPad a glass search button in the top bar expands into a field; the team switcher shrinks to an icon while it is open. Props: `query`, `searchLoading`.

**Application Detail**
- iOS / Android metadata (`platform` prop).
- Header title appears as you scroll.
- *Shared with* card: first 5 members, each with a Revoke action (trash icon + label). Revoked members are removed straight away and the next member moves up. "Show All" opens a sheet with the full list, which also has Revoke.
- *Data Linked / Not Linked to You*: privacy chips with icons (Location, Contacts, Identifiers, Contact Info, User Content, Diagnostics, Other Data, Usage Data).
- *Share sheet* (opened from the Share action):
  - App card with logo, name, version, version code and platform badge.
  - Search field that filters members of the selected team (`team` prop, default "Zylker Mobile").
  - Member list with selection circles. Selected members move to the top in the order they were picked. Members who already have access are greyed out and can't be selected.
  - Close button at top-right. A pinned Share button at the bottom stays disabled until someone is selected.
  - Sharing adds the members to *Shared with* and shows a toast.
  - `startShare` opens the sheet with 2 members already selected (used on the canvas).

**Settings**: user profile, upgrade card, organizations, teams, appearance (thumbnails show a miniature home screen in each theme) and legal links. iPad uses a split view with a sidebar; iPhone uses stacked navigation.

## Design decisions

- **Colour**: brand primary `#226DB4` (dark `#5FA8EE`) with the design system's secondary and tertiary roles (`--zh-*` tokens). Surfaces, labels and separators use the system tokens.
- **Glass buttons**: every button uses the Liquid Glass treatment (blur, inner highlight, hairline edge) for consistency.
- **Type**: Zoho Puvi, loaded locally from `assets/fonts/` because the design system's `fonts.css` doesn't wire it up. SF Pro is the fallback.
- **Icons**: drawn inline in the screens because of metadata issues in the source SVGs. Privacy icons and the trash icon come from user-supplied SF Symbol exports.
- **Sheets**: iPhone sheets are full-height with a grabber; on iPad they are centred cards (34–38px radius, sheet shadow from the design system).
- **Destructive actions**: red label and icon on a light red pill.

## Assets

```
assets/
  fonts/        Zoho Puvi Regular, Medium, Semibold, Bold
  privacy/      Privacy chip icons (location, contacts, identifiers,
                contact-info, user-content, diagnostics, other-data, usage-data)
  ill_login*.svg, ill_login_bg.png   Login illustrations (light/dark, compact)
  ill_no_org*.svg                    No Organization illustration (light/dark)
  ico_apple.png, ico_google.png      Sign-in provider marks
  zoho_logo.png                      Zoho wordmark
uploads/        Original user uploads (source for the copies above)
```

## Placeholder data

All of the following is made up and needs replacing with real data:
- App names, icons, platforms, versions, version codes and dates (Application List / Detail).
- Member names, emails and roles; team members in the Share sheet.
- Organizations, teams and the user profile (Settings).
- Confirmation copy and button labels. Check these against the brand voice.

## Known issues / next steps

- The canvas holds 51 frames and loads slowly. Split screens onto separate pages if this becomes a problem.
- The No Organization screen needs final illustrations.
- Revoke on the detail card has no confirmation step. Add one if required.
