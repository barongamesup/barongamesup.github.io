# barongamesup.github.io

Public site for Baron Mobile Games. Its job is to host the privacy policy that
Google Play and AdMob require for every published app, at a URL that never
changes.

Served by GitHub Pages from the `main` branch, root folder.

```
/                        landing page, lists every published game
/style.css               shared styling — every page links this, nothing is styled inline
/<app-slug>/privacy.html one folder per app
/_template/privacy.html  starting point for the next app — NOT published, see _config.yml
/_config.yml             keeps the template and this README out of the built site
/robots.txt
```

The repo has to be public: GitHub Pages only serves public repos on the free
plan, and the policies must be readable by Google and by users without signing
in. Nothing secret belongs here — no ad unit IDs, no keys, no keystore. The only
personal data on the site is the contact address, which Play publishes on the
store listing anyway.

Live at <https://barongamesup.github.io/>.

## Adding a new app

1. `cp -r _template <app-slug>` and rename the file to `privacy.html`
2. Replace every `{{PLACEHOLDER}}` (they are listed in a comment at the top)
3. **Read the whole policy against what the app actually does.** The template
   assumes: no account, no cloud sync, no analytics, no purchases, data stays on
   the device, ads via AdMob. Anything beyond that needs its own section — a
   policy that under-describes an app is a compliance problem, not a formality.
4. Add the app to the list in `index.html`
5. Commit and push; Pages redeploys in a minute or two
6. Paste `https://barongamesup.github.io/<app-slug>/privacy.html` into:
   - AdMob → Apps → *app* → App settings → Privacy policy URL
   - Play Console → Store listing → Privacy policy

## Why the URL matters

AdMob refuses to publish a GDPR consent message while the app it targets has no
privacy policy URL, and Play blocks the release without one. Both check the URL
is reachable, so the page must stay public and must not move once an app is
live — a dead link in a shipped app is a policy violation.

## House rules

- Keep pages plain HTML with no external requests. No CDNs, no fonts, no
  analytics; the site itself must not collect anything.
- Never delete an app's folder, even after the app is unpublished. Old installs
  still link to it.
- Update the `Last updated` date whenever the text changes.
