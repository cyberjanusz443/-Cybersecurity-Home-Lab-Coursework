# 20 — OSINT: Shodan, Google Dorks, ExifTool

Open-Source Intelligence (OSINT) exercise: discovering publicly exposed
information using only **publicly available tools** and **publicly indexed
data**. No exploitation, no unauthorized access — just reading what
organizations are already publishing without realizing it.

## What I did

### Junior tier — Google Dorks (advanced search operators)
Used Google's advanced search syntax to find documents that shouldn't be
publicly indexed:

- **`filetype:pdf "do użytku wewnętrznego"`** — found internal-use-only PDFs
  accidentally exposed on public web servers
- **`filetype:pdf "ściśle tajne"`** — surfaced strictly-confidential documents
  (test fixtures from training materials, but the technique applies)
- **`intitle:"index of" filetype:txt`** — discovered open directory listings,
  including a script labeled `panel admin`
- **`inurl:catalog.aspx`** — located library/NASA-affiliated indexable
  catalog pages with structured metadata exposed

### Medium tier — ExifTool (metadata extraction)
Extracted EXIF metadata from a sample JPEG photograph:
- **Camera model:** iPhone 14 Plus
- **Software version:** iOS 26.3.1
- **Date/time of capture:** 2026:03:26 18:39:38 (+01:00 timezone)
- **Modification date:** 2026:03:26 18:44:43
- **GPS coordinates** (when present in source — privacy risk for users
  who share photos publicly)
- **Technical EXIF data:** aperture, ISO, shutter speed, focal length

**Privacy implication:** every photo taken with a smartphone embeds
this metadata unless explicitly stripped. Posting "anonymous" photos
to public forums while preserving GPS coordinates is a documented
de-anonymization technique used in real investigations.

### Senior tier — Shodan (Internet-wide device discovery)
**Shodan** indexes banners from every Internet-facing service. Used it to
identify exposed infrastructure across categories:

**Database exposure:**
- **Unauthenticated Elasticsearch cluster** — 7.4 million documents,
  ~660 MB of data, accessible without credentials. Indices included
  named operational logs suggesting an active production system.
- **Open MongoDB instances** — multiple regions, no authentication
  required to enumerate databases and collections

**Industrial Control Systems (ICS/OT) — the most concerning findings:**
- **Siemens SIMATIC S7-1500 PLC** (firmware V3.1.1.0) on a public IP
  — same PLC family targeted by **Stuxnet** in 2010. 15 years later,
  these devices are still on the public internet.
- **Modbus devices** in Poland (port 502) — `ics` tagged on Shodan,
  indicating industrial automation gear with the SCADA-standard
  Modbus/TCP protocol exposed publicly

**IoT exposure:**
- **Unauthenticated IP camera** in France — live video stream visible
  without any authentication
- **SCADA HMI panels** — operator interfaces for industrial systems,
  some with default credentials documented in vendor manuals

**All Shodan findings have been redacted in the screenshots — real-world
IP addresses, hostnames, and organization names are masked. The
structural information (banners, protocols, exposed endpoints) is
preserved because that's what demonstrates the technique.**

## Key screenshots
- `junior_Do_Uzytku_Wewnetrznego.jpg` — Google Dork: filetype:pdf "do użytku wewnętrznego"
- `junior_Scisle_Tajne.jpg` — Google Dork: classified document discovery
- `junior_Katalog_Sieciowy_*.jpg` — Open directory listings via Google
- `junior_Skrypt_Panel_Admin.jpg` — Exposed admin panel script
- `medium_Exif_Zdjecie.jpg` — ExifTool output showing iPhone metadata
- `senior_Elasticsearch.jpg` — Unauthenticated Elasticsearch cluster (anonymized)
- `senior_MongoDB.jpg` — Open MongoDB instances (anonymized)
- `senior_Modbus_protokol_przemyslowy.jpg` — Modbus industrial device in PL (anonymized)
- `senior_Panel_Sterowania_SCADA.jpg` — Siemens SIMATIC S7-1500 PLC exposed (anonymized)
- `senior_Niezabezpieczona_Kamera.jpg` — IP camera without auth (anonymized)

## Takeaway
**OSINT is the first phase of every real attack.** Before an attacker
exploits anything, they spend hours or days enumerating targets, gathering
metadata, and mapping infrastructure. Understanding the offensive side
is fundamental to defending against it.

**Three lessons that stuck with me:**

1. **Most "leaks" are accidental publication, not active compromise.**
   Internal documents on public web servers, metrics endpoints without
   auth, unencrypted databases bound to `0.0.0.0` — these aren't hacks,
   they're misconfigurations. Defense starts with **knowing what you're
   exposing.**

2. **OT security is a real, growing crisis.** Industrial control systems
   were designed for isolated networks in the 1990s. Connecting them to
   the public Internet for "convenience" (remote diagnostics, cost cuts)
   has created a global attack surface that protective tools haven't
   caught up with. Stuxnet was 15 years ago and **the same PLC family
   is still online.**

3. **My mechatronics background is actually relevant here.** Most cybersecurity
   professionals have software/network backgrounds and view PLCs/SCADA as
   "weird hardware." Coming from mechatronics, I understand how these
   systems are deployed, why they're hard to patch (production downtime),
   and where the realistic attack vectors are. This is a **rare combination
   on the Polish market** and likely a niche I'll explore after building
   my SOC foundation.

**Ethical note on OSINT:** Everything in this exercise was done against
publicly indexed data using publicly available tools. I never attempted
to authenticate, exploit, or otherwise interact beyond reading what was
already exposed. This is the line that separates security research from
illegal intrusion — and it must never be crossed.

For an organization's defensive program: **the first action item from any
OSINT exercise is "fix what's exposed."** Shodan even provides a free
self-monitoring service — every company should be running it against
their own IP ranges weekly.
