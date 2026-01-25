# Homepage Michael Kinder

## Projektübersicht
Persönliche Bewerbungs-Homepage für Michael Kinder, gehostet auf GitHub Pages.

## Struktur
```
docs/               # GitHub Pages Verzeichnis
├── index.html      # Hauptseite (responsive, single-page)
├── impressum.html  # Impressum (§ 5 TMG)
├── datenschutz.html # Datenschutzerklärung (DSGVO)
├── profilbild.jpg
├── CNAME           # Custom Domain: michael-kinder-consulting.de
└── .nojekyll
Material/           # Quelldokumente (nicht veröffentlicht)
```

## Deployment
- Repository: https://github.com/mikinder/homepage
- Branch: main
- GitHub Pages Source: /docs
- Domain: michael-kinder-consulting.de

## Technologie
- Reines HTML/CSS/JS (keine Build-Tools)
- Responsive Design mit CSS Grid/Flexbox
- System-Fonts (keine externen Requests)
- Cookie-frei (keine Tracking, kein Google Fonts)

## Barrierefreiheit (WCAG 2.1 AA)
- Skip-Link für Tastaturnavigation
- ARIA-Labels und semantisches HTML
- Fokus-Stile für Keyboard-User
- Kontrastverhältnis mind. 4.5:1
- Zugänglicher Mobile-Menü-Button

## Inhalte
- Profil: Mobile Payment & Technology Spezialist
- Werdegang: Mastercard Advisors, Freiberuflich, CSC, IT-Dozent
- Kompetenzen: Mobile Payment, Mobile Technology, Quality Assurance
- Kontakt: E-Mail

## Rechtliches
- Impressum mit Anschrift (Dorfstr. 30a, 17328 Penkun)
- Datenschutzerklärung (GitHub Pages Hosting)

## Domain.Konfiguration
- In Github Profile Settings Domain michael-kinder-consulting.de verifiziert (ACHTUNG: nicht Repository- sondern Profile-Settings)
- In Repository > Pages die Domain michael-kinder-consulting.de verbunden
- In GoDaddy: 
	- mikinder.de: direkt auf https://mikinder.github.io/homepage/index.html umgeleitet
	- michael-kinder-consulting.de: per CNAME- und A-Params auf gitub pages konfiguriert:
                                                                                
  ┌───────┬──────┬────────────────────┐                                                                                     
  │  Typ  │ Name │        Wert        │                                                                                     
  ├───────┼──────┼────────────────────┤                                                                                     
  │ A     │ @    │ 185.199.108.153    │                                                                                     
  ├───────┼──────┼────────────────────┤                                                                                     
  │ A     │ @    │ 185.199.109.153    │                                                                                     
  ├───────┼──────┼────────────────────┤                                                                                     
  │ A     │ @    │ 185.199.110.153    │                                                                                     
  ├───────┼──────┼────────────────────┤                                                                                     
  │ A     │ @    │ 185.199.111.153    │                                                                                     
  ├───────┼──────┼────────────────────┤                                                                                     
  │ CNAME │ www  │ mikinder.github.io │                                                                                     
  └───────┴──────┴────────────────────┘           
  
 