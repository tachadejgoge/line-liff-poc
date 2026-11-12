# LINE LIFF Identity POC

Simple, frontend-only test page to retrieve the **signed-in user's LINE User ID** through a LINE OA Rich Menu. No database, backend, application secrets, or analytics. Mobile-friendly.

## Requirements

- A public **GitHub repository** (for free GitHub Pages)
- A LINE Developers account with a **LINE Login channel** and LIFF App associated with the intended provider / OA
- LIFF scopes: **profile** (optionally `openid`)

## Deploy to GitHub Pages

1. Create a **new**, unrelated GitHub repository: `line-liff-poc`. Set it **Public**. Do not use an existing OneView/CSS repo.
2. Upload `index.html`, `README.md`, and `.nojekyll` to its **main** branch root (or push this project via Git).
3. Go to **Settings → Pages → Build and deployment → Deploy from a branch**; select `main` and `/(root)`; Save.
4. Verify the GitHub Pages HTTPS URL (for owner `tachadejgoge`):
   `https://tachadejgoge.github.io/line-liff-poc/`
5. In **LINE Developers**, create a LIFF App in a LINE Login channel, set its **Endpoint URL** to the HTTPS Pages URL above, and grant **profile** scope. Full view size is convenient for testing.
6. Copy the newly created LIFF ID. Edit `index.html` in GitHub and replace only `PASTE_LIFF_ID_HERE` with the ID (e.g. `1234567890-AbCdEfGh`). **Never put a Channel Secret or access token in this file.**
7. After GitHub Pages republishes, set the Rich Menu action type to **URI**, using the **LIFF URL** `https://liff.line.me/<YOUR_LIFF_ID>`, not the raw GitHub Pages link. Test inside LINE.
8. Check User ID / Display Name / LIFF Context and optionally OA friendship. You can also use the external browser to test LINE Login.

### A note on providers

The same LINE account can yield different LINE User IDs under different providers. For integration with an existing OA, use the LINE Login channel under the **intended provider** and check the provider / OA linkage. Displaying a User ID alone does not establish its relationship to the OA's Messaging API ID.

### Privacy & security

The sample displays `liff.getProfile()` results in the user's browser. It does not save user data, send them to a backend, or expose ID/access tokens. Since GitHub Pages is publicly accessible, only use dummy/POC UI content. Avoid posting screenshots of real users' LINE IDs publicly.

### Technical implementation

One self-contained `index.html` file with the official hosted LIFF v2 SDK, basic HTML/CSS/JavaScript, `liff.init`, `liff.getProfile`, `liff.isInClient`, `liff.getContext`, and optional `liff.getFriendship`. Works without Node.js or build commands.

Official docs: https://developers.line.biz/en/reference/liff/ and https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site