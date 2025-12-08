<img width="700" height="220" alt="Skolverket MCP logo" src="https://github.com/user-attachments/assets/74563bdb-eea4-4276-a58c-ec89b11806ed" />

# Skolverket MCP Server

[![Server Status](https://img.shields.io/website?url=https%3A%2F%2Fskolverket-mcp.onrender.com%2Fhealth&label=MCP%20Server&up_message=online&down_message=offline)](https://skolverket-mcp.onrender.com/health)
[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-Published-brightgreen)](https://registry.modelcontextprotocol.io/servers/io.github.KSAklfszf921/skolverket-mcp)
[![MCP Protocol](https://img.shields.io/badge/MCP-2025--03--26-green)](https://modelcontextprotocol.io/)
[![License](https://img.shields.io/badge/license-MIT-orange)](LICENSE)

En [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) server som ger AI-assistenter tillgång till **alla Skolverkets öppna API:er** – Läroplan API, Skolenhetsregistret och Planned Educations API. Genom att ansluta till MCP-servern kan du med hjälp av AI söka, hitta, jämföra och analysera all data och statistik som finns tillgängligt i Skolverkets öppna databaser. 

---

## Snabbstart 

Det är enkelt att ansluta en LLM / AI-chatbot till MCP-servern. Anslut antingen direkt till den hostade servern (enkelt och smidigt) eller installera lokalt. Nedan finner du guider för olika klienter.



<details>


<summary><strong>1. AI-chatbotar</strong></summary>
<details>
  
<summary><strong>ChatGPT (Web)</strong></summary>
  
--- 

1. Öppna inställningar och aktivera Developer Mode
2. Skapa ny anslutning med URL: `https://skolverket-mcp.onrender.com/mcp` 

#### Videoguide (tryck play)
![ChatGPT anslutning till MCP](https://github.com/user-attachments/assets/eb99a8ad-2154-4a58-b13f-c1edb57dbf47)


</details>

<details>
<summary><strong>Claude (Web)</strong></summary>
  
--- 

**1. Gå till claude.ai:**
- Logga in på https://claude.ai

**2. Öppna inställningar:**
- Klicka på din profil (nere till vänster)
- Välj **"Settings"**

**3. Lägg till MCP-server:**
- Gå till **"Developer"** eller **"Integrations"**
- Klicka **"Add MCP Server"** eller **"Connect"**
- **Name:** `Skolverket MCP`
- **URL:** `https://skolverket-mcp.onrender.com/mcp`
- Klicka **"Connect"** eller **"Add"**

#### Videoguide (tryck play)
https://github.com/user-attachments/assets/9ded5a37-c168-4ab4-8bac-cca2a4195628

---

</details>

</details>
<img width="189" height="38" alt="claude chatgpt" src="https://github.com/user-attachments/assets/20a29640-40e0-43f1-8b0b-c3f6adae691a" />

---

<details>
---


<summary><strong>1. Lokal installation</strong></summary>



<details>
<summary><strong>Claude Desktop</strong></summary>
  

**1. Klona och bygg:**
```bash
git clone https://github.com/KSAklfszf921/skolverket-mcp.git
cd skolverket-mcp
npm install && npm run build
```

**2. I Claude Desktop:**
- Settings → **Developer** (inte Connectors!)
- Klicka **"Edit Config"**

**3. Lägg till i JSON-filen:**
```json
{
  "mcpServers": {
    "skolverket": {
      "command": "node",
      "args": ["/absolut/sökväg/till/skolverket-mcp/dist/index.js"]
    }
  }
}
```

**4. Spara och starta om Claude Desktop**

**Notera:** Lokal installation använder stdio-transport via Developer-sektionen, inte Connectors.

</details>

<details>
<summary><strong>Claude Code</strong></summary>
  

**Live-Server:**
```bash
claude mcp add --transport http skolverket https://skolverket-mcp.onrender.com/mcp
```

**Lokal (från källkod):**
```bash
# Efter git clone och npm install (se ovan)
claude mcp add skolverket node /absolut/sökväg/till/dist/index.js
```

**Verifiera:** `claude mcp list`

</details>

<details>
<summary><strong>OpenAI Codex</strong></summary>
  
#### Remote Server (HTTP)

**`~/.codex/config.toml`:**
```toml
[mcp.skolverket]
url = "https://skolverket-mcp.onrender.com/mcp"
transport = "http"
```

**1. Klona och bygg (om ej redan gjort):**
```bash
git clone https://github.com/KSAklfszf921/skolverket-mcp.git
cd skolverket-mcp
npm install && npm run build
```

**2. Konfigurera stdio-transport:**

**`~/.codex/config.toml`:**
```toml
[mcp.skolverket]
command = "node"
args = ["/absolut/sökväg/till/skolverket-mcp/dist/index.js"]
transport = "stdio"
```

**Windows:**
```toml
[mcp.skolverket]
command = "node"
args = ["C:\\Users\\username\\skolverket-mcp\\dist\\index.js"]
transport = "stdio"
```
</details>
</details>


<img width="273" height="46" alt="claudecode openaicodex googlegemini" src="https://github.com/user-attachments/assets/c4c73367-e0f5-408a-a074-83b7ce45805c" />



---

## Funktioner

Servern kopplar till tre av Skolverkets öppna API:er:

**1. Syllabus API**
Läroplaner (LGR22, GY25 m.m.), ämnen, kurser, gymnasieprogram med kunskapskrav och centralt innehåll.

**2. Skolenhetsregistret**
Sök och filtrera skolor, förskolor och andra skolenheter. Inkluderar aktiva, nedlagda och vilande enheter.

**3. Planned Educations API**
Yrkeshögskola, SFI, Komvux och andra vuxenutbildningar med startdatum, platser och studietakt.

#### Verktyg (tools)
MCP-servern implementerar MCP-protokollet med stöd för:
- **41 verktyg** – 17 Syllabus API, 4 School Units, 17 Planned Educations (inkl. gymnasieutbildningar, statistik, dokument), 3 Support Data, 1 diagnostik
- **4 resurser** – API-info, skoltyper, läroplanstyper, kurs- och ämneskoder
- **5 promptmallar** – Kursanalys, versionsjämförelser, vuxenutbildning, studievägledning, kursplanering



---


## Användningsområden


https://github.com/user-attachments/assets/8eefa26c-4162-49a5-adf0-82677a663b19


### För Lärare
- **Kursplanering:** "Jämför kunskapskraven E och A för Svenska 1 och ge förslag på bedömningsuppgifter"
- **Tematiskt arbete:** "Hitta alla kurser i gymnasiet som har hållbarhet i sitt centrala innehåll"
- **Bedömning:** "Visa alla kunskapskrav för betyg C i Biologi 1 och förklara skillnaderna mot B"

### För elever & föräldrar
- **Programval:** "Jämför Naturvetenskapsprogrammet och Teknikprogrammet - vilka kurser är obligatoriska?"
- **Kursval:** "Vilka matematikkurser finns på gymnasiet och vilka bygger på varandra?"
- **Betygskriterier:** "Vad krävs för att få A i Historia 1a1?"

### För undersökningar & analyser  
- **Skolregister:** "Hitta alla aktiva gymnasieskolor i Stockholms län"
- **Kursutbud:** "Vilka skolor erbjuder Ekonomiprogrammet i Malmö?"
- **Läroplansanalys:** "Analysera hur begreppet 'programmering' har utvecklats i läroplaner 2011-2025"

---

## Övrigt
**Skapad av:** [Isak Skogstad](mailto:isak.skogstad@me.com) • [X/Twitter](https://x.com/isakskogstad)

[![MCP Badge](https://lobehub.com/badge/mcp/ksaklfszf921-skolverket-syllabus-mcp)](https://lobehub.com/mcp/ksaklfszf921-skolverket-syllabus-mcp)

---

## 📝 Licens

MIT License – Data från Skolverkets öppna API:er. Inte officiellt associerad med Skolverket.
