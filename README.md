# Sportduell

Wöchentliches Sportduell als installierbare Web-App (PWA). Daten in Supabase, Hosting über GitHub Pages.

## Dateien

| Datei | Zweck |
|---|---|
| `index.html` | Die App (Oberfläche + Logik) |
| `config.js` | Supabase-URL und anon-Key |
| `supabase.js` | Supabase-Bibliothek (v2.117.3), lokal für Offline-Start |
| `sw.js` | Service Worker: Offline-Cache. Bei Änderungen `VERSION` hochzählen |
| `manifest.webmanifest`, `icons/` | App-Name, Icon, Vollbild |
| `supabase-setup.sql` | Tabellen, Zugriffsregeln, Startdaten. Nur einmal in Supabase ausführen, **nicht** nötig im Repo |

## Einrichtung

1. **SQL:** In `supabase-setup.sql` Julians E-Mail eintragen (Abschnitt 5). Dann in Supabase *SQL Editor → New query*, alles einfügen und *Run*.
2. **E-Mail-Code aktivieren:** *Authentication → Emails → Templates → Magic Link*. Im Text diese Zeile ergänzen:
   `<p>Dein Code: <b>{{ .Token }}</b></p>`
   (Ohne den Code würde der Link in Safari statt in der installierten App einloggen.)
3. **GitHub:** Alle Dateien außer `supabase-setup.sql` ins Repo hochladen. *Settings → Pages → Source: Deploy from a branch → main / (root) → Save.*
   Nach ca. 1 Minute läuft die App unter `https://<benutzername>.github.io/<repo>/`.
4. **Supabase-URL hinterlegen:** *Authentication → URL Configuration → Site URL* auf die GitHub-Pages-Adresse setzen.
5. **Installieren:** Adresse am Handy öffnen (iPhone: Safari), anmelden, „Zum Home-Bildschirm“.

## Regeln in der Datenbank

- Nur die zwei E-Mail-Adressen in der Tabelle `players` sehen Daten.
- Jeder trägt nur für sich selbst ein und löscht nur eigene Einträge.
- Namen, Körpergewicht, Punktwerte und Deckel dürfen beide ändern.
- E-Mail-Adresse ändern: in Supabase unter *Table Editor → players*.
