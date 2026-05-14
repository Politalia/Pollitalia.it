# Changelog

Tutte le modifiche significative a Pollitalia sono documentate qui.
Formato: [Keep a Changelog](https://keepachangelog.com/it/1.0.0/).
Versioning: [Semantic Versioning](https://semver.org/).

---

## [Unreleased]

---

## [1.0.2] — 2026-05-14

### Fixed
- Overscroll bloccato oltre il fondo su Chrome mobile (`overscroll-behavior-y: none` su `html`)

### Changed
- Versione hardcoded aggiornata a v1.0.2 in `index.html` e `profile.html`

---

## [1.0.1] — 2026-05-08

### Security
- **H1**: `escapeHtml()` su titoli mercati in admin, index, barometro, lega — prevenzione XSS stored
- **H2**: rimossa auto-escalation `isAdmin` client-side da `admin.html`
- **H3**: rotazione chiave EmailJS
- **M1**: security headers HTTP in `firebase.json` (HSTS, X-Frame-Options, nosniff, Referrer-Policy)
- **M2**: fix open redirect — validazione same-origin su link notifiche
- **M3**: regola Firestore `leagues/update` limitata a `hasOnly(['members'])`
- **L1**: regola Firestore `wallets/update` limitata a `owner || isLeagueAdmin`
- **C1**: bonus referral spostato su Cloud Function `onUserCreated`, rimossa rule client-side
- **C2**: XSS stored notifiche — `escapeHtml` su message, regola 500 chars, link via data-attribute
- **C0**: `users/create` blocca `isAdmin==true` e `points>550`; `users/update` blocca `points/totalBets/wonBets`
- **C0b**: `onUserCreated` usa `db.runTransaction()` per idempotency atomica (no race condition doppio bonus)
- **N1**: `notifications/create` richiede `userId == auth.uid` — blocca spam verso altri utenti

### Fixed
- Admin premi: `stripHtml()` al load per pulire HTML salvato erroneamente in Firestore
- Animazioni hero su bfcache Safari (`pageshow persisted` — reset display e keyframes)
- Overflow-x su body — blocca scroll orizzontale su PWA mobile

---

## [0.9.2] — 2026-05-08

### Added
- `deploy.sh` con aggiornamento automatico di `DEPLOY_LOG.md` e versione hardcoded

### Fixed
- Versione v0.9.2 in `index.html` (`sed` corretto nel deploy script)

---

## [0.9.1] — 2026-05-06

### Added
- Notifiche sondaggi con deep-link — like/voto/commento aprono il sondaggio diretto
- Sondaggi multi-tipo: Sì/No (retrocompatibile) e Multi-scelta 2-4 opzioni con palette colori

### Fixed
- Chat sondaggi non si chiudeva dopo un commento — ripristino chat aperte post re-render
- `event.preventDefault()` su Enter nei commenti sondaggi — evitava reload pagina
- Bottom nav sondaggi: rimosso `transform: none` che impediva GPU compositing
- `polls-grid`: rimosso `display:none;display:flex` duplicato

---

## [0.9.0] — 2026-04-28

### Added
- Sistema referral — codice univoco per utente, +50 crediti per entrambi
- Cookie banner GDPR — Accetta/Rifiuta, scadenza 6 mesi
- FAQ page con schema markup FAQPage (JSON-LD)
- Sezione FAQ in sondaggi

### Fixed
- Icona P duplicata in navbar su 7 pagine — rimosso duplicato
- `nav-brand` class su `<div>` invece di `<a>` — flex non applicato (7 pagine)
- Share card profilo obsoleta — riscritta con canvas, font Syne, logo tricolore, moneta PNG
- `points-badge` con moneta duplicata — rimossa da HTML statico (JS già la inietta)
- Mobile navbar overflow — `brand-logo` nascosto a ≤768px, solo icona P visibile
- Google OAuth `redirect_uri_mismatch` — aggiunto `pollitalia.it` in Firebase Auth e Google Cloud

### Changed
- Hero homepage: countdown al lancio + copy waiting list (modalità pre-lancio)

---

## [0.8.0] — 2026-04-21

### Added
- Aurora borealis hero background con scroll parallax CSS
- Animazioni scroll reveal con IntersectionObserver (`js/ui.js`)
- `animateCounter` globale per contatori animati
- Push Notifications (FCM) — guard `_pushInitDone`, cleanup vecchio SW

### Changed
- Mercati demo statici sulla landing (nessuna query Firestore live per visitatori)
- Barometro D3.js: alias `GEO_ALIASES` per "Trentino-Alto Adige/Südtirol"
- Bottom nav: rimosso link Admin per non-admin su tutte le pagine

### Fixed
- Scroll position: `history.scrollRestoration = 'manual'` + `window.scrollTo(0,0)` in index
- Ricarica mensile Invalid Date: `new Date(new Date(now).setMonth(...))`
- Chrome lag: `navGlow` solo opacity, rimosso `background-position` animation
- Gradient text su header pagine inner

---

## [0.1.0] — 2026-04-09

### Added
- Prima versione pubblica: Pollitalia prediction market politico italiano
- Mercati parimutuel con scommesse
- Leghe private con wallet separati
- Sondaggi social con filtri (regione / trending / voti)
- Notifiche real-time con badge
- Classifica generale e mensile (podio fisso a 3 slot)
- Premi sponsor mensili configurabili dall'admin
- Hall of Fame — campione del mese
- PWA (Progressive Web App)
- Chat con likes su mercati e leghe
- Barometro politico D3.js
- Ricarica mensile automatica +100 crediti
- Pannello admin con gestione mercati, utenti, premi

---

[Unreleased]: https://github.com/Pietro-Dragoni/politalia/compare/v1.0.2...HEAD
[1.0.2]: https://github.com/Pietro-Dragoni/politalia/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/Pietro-Dragoni/politalia/compare/v0.9.2...v1.0.1
[0.9.2]: https://github.com/Pietro-Dragoni/politalia/compare/v0.9.1...v0.9.2
[0.9.1]: https://github.com/Pietro-Dragoni/politalia/compare/v0.9.0...v0.9.1
[0.9.0]: https://github.com/Pietro-Dragoni/politalia/compare/v0.8.0...v0.9.0
[0.8.0]: https://github.com/Pietro-Dragoni/politalia/compare/v0.1.0...v0.8.0
[0.1.0]: https://github.com/Pietro-Dragoni/politalia/releases/tag/v0.1.0
