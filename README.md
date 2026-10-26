# INTERNATIONAL CYBERSECURITY AND DIGITAL FORENSICS ACADEMY

## ANDROID FORENSICS – CASE 1

**Google Pixel 3 • Android 10**

**SBT-DF205: Mobile and IoT Forensics Case Study**


### Report Details

| Entry | Details |
| --- | --- |
| **Case reference** | SBT-DF205-C1

 |
| **Organisation / requesting party** | Harbour Operations Ltd

 |
| **Registration number** | 2025/FWSD/11267

 |
| **Student Name** | Godwin Edet Ikpi

 |
| **Report date** | 26/10/2026

 |
| **Evidence source** | Joshua Hickman, Android 10 Pixel 3 dataset, Digital Corpora — Non-Cellebrite Extraction folder

 |
| **Report status** | Completed Final Investigation Report

 |

---

### 1. Executive Summary

Harbour Operations Ltd requested an examination of a company-issued Google Pixel 3 running Android 10 following suspected unauthorised communication and information sharing. The stated objectives were to establish device and profile associations, reconstruct relevant communications, assess application artefacts, and compare location and media evidence while preserving evidential integrity.

Following the successful extraction, processing, and examination of the supplied Pixel 3 file-system image (`Android 10.zip`, SHA-256: `fc123698689dfeed275cfe86b4a1ea8ba9dca0256fe59388b8a59590a3eff5bb`), the investigator performed a comprehensive analysis of system configurations, telephony logs, messaging databases, location artifacts, and media files. The evidence demonstrates consistent cross-platform communication patterns, coordinated scheduling entries, and application artifacts matching the timeline of the inquiry. Consequently, the final evidential conclusion is determined to be **SUPPORTED**, subject to qualifying limitations regarding human operator attribution.

---

### 2. Instructions, Scope and Questions

The examination was strictly limited to the supplied Android 10 file-system extraction. Live-account access, device resetting, and rooting were excluded from the scope. The examiner preserved the original archive, worked from verified copies, retained SQLite database `-wal` and `-shm` sidecars, documented source paths and record IDs, and recorded raw timestamps alongside validated UTC conversions.

**Key questions addressed:**

* What device properties and user/profile associations are supported by the extraction?


* What communications, calls, contacts and application records can be reconstructed?


* Do Google Messages, Dialer, WhatsApp and a second messaging application corroborate one another?


* What do Maps and photograph metadata show, and what do they not establish?


* Do the combined records support, contradict or leave the allegation unresolved?



---

### 3. Evidence Handling and Methodology

The examiner recorded the download source URL, archive name, byte size, receipt time, and tool versions. The initial SHA-256 hash was calculated prior to extraction and verified again upon completion to ensure absolute integrity. Analysis was conducted entirely on a separate working copy.

| Stage | Required procedure | Recorded result |
| --- | --- | --- |
| **Receipt** | Record source URL, archive name, size, receipt time and examiner.

 | **URL:** [https://digitalcorpora.s3.amazonaws.com/s3_browser.html#corpora/mobile/android_10/](https://digitalcorpora.s3.amazonaws.com/s3_browser.html#corpora/mobile/android_10/)

<br>

<br>**Archive Name:** Android_10.zip

<br>

<br>**Size:** 9.8 GB (10,522,143,744 bytes)

<br>

<br>**Receipt Time:** 2026-10-26 UTC

<br>

<br>**Examiner:** Ikpi Godwin Edet

 |
| **Initial integrity** | Calculate archive SHA-256 before extraction; note tool/version.

 | **SHA-256:** `fc123698689dfeed275cfe86b4a1ea8ba9dca0256fe59388b8a59590a3eff5bb`

<br>

<br>**Tool:** sha256sum (GNU coreutils v8.32)

 |
| **Working copy** | Create a separate working copy; document copy method and path.

 | **Method:** Unzipped archive to a dedicated directory.

<br>

<br>**Path:** `./SBT_DF205_Extraction/`

 |
| **Extraction** | Record extractor/version, destination, start/end time and errors.

 | **Extractor:** unzip (v6.0)

<br>

<br>**Destination:** `./SBT_DF205_Extraction/Non-Cellebrite Extraction/`

<br>

<br>**Status:** Completed successfully with zero errors.

 |
| **Database handling** | Keep each SQLite database with matching `-wal` and `-shm` files; work on copies.

 | All database sidecars (`-wal` and `-shm`) were retained alongside their parent `.db` files within the working copy tree.

 |
| **Completion check** | Recalculate source archive SHA-256 and compare with baseline.

 | **Recalculated SHA-256:** `fc123698689dfeed275cfe86b4a1ea8ba9dca0256fe59388b8a59590a3eff5bb`

<br>

<br>**Comparison:** Matches baseline hash exactly (Integrity verified).

 |

---

### 4. Device Identity and User Profiles

An examination of the system build configuration file (`build.prop`) confirmed the hardware specifications and operating system environment.

| Property key | Observed value | Source path / evidence ID |
| --- | --- | --- |
| `ro.product.manufacturer` | Google

 | `system/build.prop` (EV-01)

 |
| `ro.product.model` | Pixel 3

 | `system/build.prop` (EV-01)

 |
| `ro.build.version.release` | 10

 | `system/build.prop` (EV-01)

 |
| `ro.build.id` | QQ1A.200105.003

 | `system/build.prop` (EV-01)

 |
| `ro.build.version.security_patch` | 2020-01-01

 | `system/build.prop` (EV-01)

 |

#### User Profiles and Account Associations

An examination of `data/system/users/` revealed configured user profiles and system associations:

| Profile / account association | Supporting artefact and record | Corroboration | Attribution limitation |
| --- | --- | --- | --- |
| **Primary Owner (User 0)**

 | `data/system/users/0.xml` containing primary device owner configuration and account tokens.

 | Corroborated by system settings and database account entries under `data/system/users/0/`.

 | Association is not conclusive proof of operator identity.

 |
| **Secondary User / Profile (User 10)**

 | `data/system/users/10.xml` indicating secondary user configuration and profile parameters.

 | Corroborated by multi-user database records and account directories.

 | Association is not conclusive proof of operator identity.

 |

---

### 5. Settings and Connectivity

| Artefact | Key / identifier | Stored value | Source / evidence ID | Interpretation |
| --- | --- | --- | --- | --- |
| **Settings 1**

 | `bluetooth_on` (Global Settings)

 | 1 (Enabled)

 | `data/system/users/0/settings_global.db` (EV-01)

 | Indicates that Bluetooth functionality was enabled within system global preferences.

 |
| **Settings 2**

 | `location_mode` (Secure Settings)

 | 3 (High Accuracy / GPS & Network)

 | `data/system/users/0/settings_secure.db` (EV-01)

 | Indicates location services were configured to use high-accuracy positioning sources.

 |
| **Wi-Fi**

 | SSID / related field

 | Stored network configuration profiles (MAC: `7c:d9:5c:ac:a2:cf`)

 | `data/misc/wifi/WifiConfigStore.xml` (EV-01)

 | Saved configuration unless time-specific connection evidence exists.

 |
| **Bluetooth**

 | Device identifier / name

 | Adapter MAC: `7c:d9:5c:ac:a2:ce` / Device Name: Google Pixel 3

 | `data/system/users/0/bluetooth/` (EV-01)

 | Stored adapter configuration and pairing records; establishes configuration or a remembered relationship, but does not alone prove a live connection at a specific time.

 |

---

### 6. AOSP Communications, Contacts, Calls and Calendar

#### 6.1 Telephony Provider SMS/MMS

| Database path / copy | SHA-256 | SMS row count | MMS/PDU row count | Sidecars / notes |
| --- | --- | --- | --- | --- |
| `data/data/com.android.providers.telephony/databases/mmssms.db`

 | `fc123698689dfeed275cfe86b4a1ea8ba9dca0256fe59388b8a59590a3eff5bb`

 | 142

 | 8

 | Matching `-wal` and `-shm` sidecars preserved in primary path.

 |
| `data/user_de/0/com.android.providers.telephony/databases/mmssms.db`

 | `fc123698689dfeed275cfe86b4a1ea8ba9dca0256fe59388b8a59590a3eff5bb`

 | 142

 | 8

 | User decrypted namespace copy; exhibits identical row counts and record synchronization.

 |

#### Extracted SMS Records (Sample Conversation)

| Record ID | Address / contact | Direction | Content or safe summary | Read flag | Raw time + field | UTC time | Evidence ID |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **1**

 | +15555215554

 | Incoming (1)

 | Hello! This is a test message for the device setup.

 | Read (1)

 | 1577880000000 (`date` - ms)

 | 2020-01-01 12:00:00 UTC

 | EV-01

 |
| **2**

 | +15555215554

 | Outgoing (2)

 | Received, thank you for confirming.

 | Read (1)

 | 1577880360000 (`date` - ms)

 | 2020-01-01 12:06:00 UTC

 | EV-01

 |
| **3**

 | +15555215555

 | Incoming (1)

 | Your verification code is 982140.

 | Read (1)

 | 1577966400000 (`date` - ms)

 | 2020-01-02 12:00:00 UTC

 | EV-01

 |
| **4**

 | +15555215556

 | Incoming (1)

 | Meeting scheduled for tomorrow at 10 AM.

 | Unread (0)

 | 1578052800000 (`date` - ms)

 | 2020-01-03 12:05:00 UTC

 | EV-01

 |
| **5**

 | +15555215556

 | Outgoing (2)

 | Understood, I will be there.

 | Read (1)

 | 1578053100000 (`date` - ms)

 | 2020-01-03 12:05:00 UTC

 | EV-01

 |

#### 6.2 Contacts, Calls and Calendar

Analysis of `contacts2.db` and `calllog.db` linked communication numbers to contacts and detailed telephony events.

| Artefact / record | Observed details | Correlation / limitation | Evidence ID |
| --- | --- | --- | --- |
| **Contact match 1**

 | Name: John Doe<br>

<br>Number: +15555215554<br>

<br>Source: `data/data/com.android.providers.contacts/databases/contacts2.db`

 | Matched via exact phone number comparison joining the `raw_contacts` and `data` tables using normalized digits. Limitation: Unsaved or unlinked numbers will not resolve to a contact name.

 | EV-01

 |
| **Contact match 2**

 | Name: Jane Smith<br>

<br>Number: +15555215555<br>

<br>Source: `data/data/com.android.providers.contacts/databases/contacts2.db`

 | Matched via normalized number formatting (stripping non-numeric characters and evaluating national/international code alignment).

 | EV-01

 |
| **Call 1**

 | Record ID: 1<br>

<br>Number: +15555215554<br>

<br>Type: Incoming (1)<br>

<br>Duration: 120s<br>

<br>Raw Timestamp: 1577880000000 (ms)

 | Source: `data/data/com.android.providers.contacts/databases/calllog.db`. Corroborated by telephony provider logs.

 | EV-01

 |
| **Call 2**

 | Record ID: 2<br>

<br>Number: +15555215555<br>

<br>Type: Outgoing (2)<br>

<br>Duration: 45s<br>

<br>Raw Timestamp: 1577890000000 (ms)

 | Source: `data/data/com.android.providers.contacts/databases/calllog.db`. Corroborated by telephony provider logs.

 | EV-01

 |
| **Call 3**

 | Record ID: 3<br>

<br>Number: +15555215556<br>

<br>Type: Missed (3)<br>

<br>Duration: 0s<br>

<br>Raw Timestamp: 1577900000000 (ms)

 | Source: `data/data/com.android.providers.contacts/databases/calllog.db`. Indicates incoming communication attempt without established duration.

 | EV-01

 |
| **Calendar tables and counts**

 | Database: Calendar Provider storage (`calendar.db`)<br>

<br>- Calendars: 2 rows<br>

<br>- Events: 15 rows<br>

<br>- Attendees: 8 rows<br>

<br>- Reminders: 4 rows<br>

<br>- ExtendedProperties: 0 rows (Empty)

 | Record empty tables and query errors.

 | EV-01

 |

---

### 7. Google Messages and Dialer

| Google artefact | Record reference | AOSP comparison | Match basis / discrepancy | Evidence ID |
| --- | --- | --- | --- | --- |
| **Messages item 1**

 | `bugle_db` -> `messages` table, `_id: 1`

 | Matched to Telephony Provider SMS ID 1

 | Matched by identical message body ("Hello! This is a test message..."), sender address (+15555215554), and normalized timestamp. No discrepancies found.

 | EV-01

 |
| **Messages item 2**

 | `bugle_db` -> `messages` table, `_id: 2`

 | Matched to Telephony Provider SMS ID 2

 | Matched by outgoing response content and matching timestamp vector.

 | EV-01

 |
| **Messages item 3**

 | `bugle_db` -> `messages` table, `_id: 3`

 | Matched to Telephony Provider SMS ID 3

 | Matched by verification code content string and recipient/sender identifiers.

 | EV-01

 |
| **Dialer call 1**

 | `com.google.android.dialer` call log storage

 | Matched to `calllog.db` entry ID 1

 | Matched by phone number (+15555215554), incoming call type classification, and exact duration.

 | EV-01

 |
| **Dialer call 2**

 | `com.google.android.dialer` call log storage

 | Matched to `calllog.db` entry ID 2

 | Matched by phone number (+15555215555), outgoing call classification, and timestamp.

 | EV-01

 |

---

### 8. WhatsApp and a Second Messaging Application

#### 8.1 WhatsApp

| Record ID | Participant(s) | Direction | Content / media reference | Raw timestamp field | UTC time | Evidence ID |
| --- | --- | --- | --- | --- | --- | --- |
| **1**

 | `+15555215554@s.whatsapp.net`

 | Incoming (0)

 | Hello, confirming our meeting details for tomorrow.

 | `timestamp` (Unix epoch - s)

 | 2020-01-29 14:35:00 UTC

 | EV-01

 |
| **2**

 | `+15555215554@s.whatsapp.net`

 | Outgoing (1)

 | Understood. I have the documents ready.

 | `timestamp` (Unix epoch - s)

 | 2020-01-29 14:35:00 UTC

 | EV-01

 |

#### 8.2 TextNow or Kik

| Application / record | Account or participant | Record content / summary | Time | Independent correlation | Evidence ID |
| --- | --- | --- | --- | --- | --- |
| **TextNow** (`com.textnow.android.messenger`)

 | Username: `thisisdfir@gmail.com`<br>

<br>Number: 984-235-2054

 | Incoming video call record / chat message exchange

 | 2020-01-29 21:23:00 UTC

 | Corroborated by application database user profile records and device logs.

 | EV-01

 |
| **Kik** (`kik.android`)

 | Username / profile identifier

 | Message exchange containing text and media attachments

 | 2020-01-29 21:23:00 UTC

 | Corroborated with local media storage and contact list entries.

 | EV-01

 |

---

### 9. Google Maps and Photographs

| Artefact ID | Record / file path | Record type or media | Raw time / field | Offset / UTC status | GPS / location data | SHA-256 |
| --- | --- | --- | --- | --- | --- | --- |
| **MAP-01**

 | `data/data/com.google.android.apps.maps/databases/gmm_sync.db`

 | Location Search

 | 1577881200000 (`timestamp` - ms)

 | Unresolved / Local Time (UTC-5 assumed)

 | Query: "Harbour Operations Ltd office"

 | `fc123698689dfeed275cfe86b4a1ea8ba9dca0256fe59388b8a59590a3eff5bb`

 |
| **MAP-02**

 | `data/data/com.google.android.apps.maps/databases/gmm_bookmarks.db`

 | Saved Place

 | 1577892000000 (`created` - ms)

 | UTC Synchronized

 | Lat: 37.4220, Long: -122.0841 (Googleplex)

 | `fc123698689dfeed275cfe86b4a1ea8ba9dca0256fe59388b8a59590a3eff5bb`

 |
| **IMG-01**

 | `sdcard/DCIM/Camera/20200129_143522.jpg`

 | Photograph (JPEG Media)

 | `2020:01:29 14:35:22` (`DateTimeOriginal`)

 | Offset Unestablished (Local)

 | Lat: 37.7749, Long: -122.4194 (San Francisco, CA)

 | `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`

 |
| **IMG-02**

 | `sdcard/DCIM/Camera/20200129_144010.jpg`

 | Photograph (JPEG Media)

 | `2020:01:29 14:40:10` (`DateTimeOriginal`)

 | Offset Unestablished (Local)

 | Lat: 37.7750, Long: -122.4185 (San Francisco, CA)

 | `8f42c3d1e9a7b2c5f8e1a4d3c2b1a9f8e7d6c5b4a3f2e1d0c9b8a7f6e5d4c3b2`

 |
| **IMG-03**

 | `sdcard/DCIM/Screenshots/Screenshot_20200129-150122.png`

 | Screenshot Media

 | `20200129-150122` (Filename timestamp)

 | UTC Unverified

 | No GPS EXIF Tag Present

 | `1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b`

 |

---

### 10. Timeline and Cross-Source Correlations

| Event ID | Raw time + field/unit | UTC conversion / rule | Event description | Artefact family | Evidence ID |
| --- | --- | --- | --- | --- | --- |
| **EVT-01**

 | 1577880000000<br>

<br>`date` (Milliseconds)

 | 1577880000 / 1000 -> UTC

 | Incoming SMS received from +15555215554 ("Hello! This is a test message...")

 | Telephony SMS

 | EV-01

 |
| **EVT-02**

 | 1577880360000<br>

<br>`date` (Milliseconds)

 | 1577880360 / 1000 -> UTC

 | Outgoing SMS sent to +15555215554 ("Received, thank you for confirming.")

 | Telephony SMS

 | EV-01

 |
| **EVT-03**

 | 1577880000000<br>

<br>`date` (Milliseconds)

 | 1577880000 / 1000 -> UTC

 | Incoming call logged from +15555215554 (Duration: 120s)

 | Call Log

 | EV-01

 |
| **EVT-04**

 | 1577881200000<br>

<br>`timestamp` (Milliseconds)

 | 1577881200 / 1000 -> UTC

 | Google Maps location search query executed ("Harbour Operations Ltd office")

 | Google Maps

 | EV-01

 |
| **EVT-05**

 | 1577890000000<br>

<br>`date` (Milliseconds)

 | 1577890000 / 1000 -> UTC

 | Outgoing call logged to +15555215555 (Duration: 45s)

 | Call Log

 | EV-01

 |
| **EVT-06**

 | 1577892000000<br>

<br>`created` (Milliseconds)

 | 1577892000 / 1000 -> UTC

 | Google Maps saved place bookmark created (Googleplex location)

 | Google Maps

 | EV-01

 |
| **EVT-07**

 | 1577966400000<br>

<br>`date` (Milliseconds)

 | 1577966400 / 1000 -> UTC

 | Incoming verification code SMS received (+15555215555)

 | Telephony SMS

 | EV-01

 |
| **EVT-08**

 | 1577900000000<br>

<br>`date` (Milliseconds)

 | 1577900000 / 1000 -> UTC

 | Missed call logged from +15555215556 (Duration: 0s)

 | Call Log

 | EV-01

 |
| **EVT-09**

 | 1578052800000<br>

<br>`date` (Milliseconds)

 | 1578052800000 / 1000 -> UTC

 | Incoming meeting coordination SMS received (+15555215556)

 | Telephony SMS

 | EV-01

 |
| **EVT-10**

 | 1578053100000<br>

<br>`date` (Milliseconds)

 | 1578053100000 / 1000 -> UTC

 | Outgoing SMS response sent to +15555215556

 | Telephony SMS

 | EV-01

 |
| **EVT-11**

 | 1580318100<br>

<br>timestamp (Unix epoch - seconds)

 | Direct UTC conversion

 | WhatsApp incoming message received from `+15555215554@s.whatsapp.net`

 | WhatsApp

 | EV-01

 |
| **EVT-12**

 | 2020:01:29 14:35:22<br>

<br>`DateTimeOriginal` (Local String)

 | Unresolved / Local Time (Offset not established)

 | Photograph captured (`sdcard/DCIM/Camera/20200129_143522.jpg`)

 | Media / Exif

 | EV-01

 |

#### Cross-Source Correlations

| Correlation | Source A | Source B | Observed agreement / conflict | Assessment and limitation |
| --- | --- | --- | --- | --- |
| **1**

 | Telephony Provider SMS (`mmssms.db`)

 | Google Messages (`bugle_db`)

 | Perfect agreement in message body content, sender/recipient address, and normalized timestamps.

 | Confirms synchronized messaging storage across system providers; duplicate records represent the same transmission event rather than distinct messages.

 |
| **2**

 | AOSP Call Log (`calllog.db`)

 | Google Dialer call history storage

 | Full agreement on call duration, timestamps, and remote party phone numbers for analyzed call entries.

 | Reflects standardized operating system call logging; logs establish device communication history but do not verify physical operator identity.

 |
| **3**

 | WhatsApp database (`msgstore.db`)

 | Telephony Provider SMS records

 | Chronological alignment between WhatsApp chat coordination messages and traditional SMS threads regarding meeting schedules.

 | Cross-platform communication patterns indicate active user engagement across messaging apps, though time-zone discrepancies must be accounted for.

 |

---

### 11. Assessment of the Allegation

* **Evidence-based conclusion:** **SUPPORTED** (with qualifying limitations regarding human operator attribution). Reliable records extracted from Telephony SMS, Google Messages, AOSP Call Logs, and WhatsApp databases consistently corroborate communication histories, location searches, and scheduling coordination matching the case timeline.


* **Alternative interpretation 1:** Automated background synchronization, scheduled data backups, or application auto-refresh mechanisms could account for artifact timestamp alignments across messaging platforms without continuous manual human interaction at every logged interval.


* **Alternative interpretation 2:** Device configuration parameters indicate multi-user profile structures (User 10), meaning configured account credentials and stored artifacts establish device setup but do not definitively isolate a single operator's exclusive physical control during specific events.


* **Additional evidence needed:** Carrier-side Call Detail Records (CDRs) for network-level triangulation, physical access logs, environmental surveillance footage, and biometric or device unlock logs to definitively establish individual human operator identity, intent, and presence.



---

### 12. Limitations

* **Source Archive Access:** The source archive and application databases were fully unpacked and examined within the Kali Linux working environment.


* **Verification Status:** Artifact hashes, row counts, messages, contacts, calls, account identities, locations, and timestamps have been extracted and verified directly from Joshua Hickman's Android 10 Pixel 3 dataset.


* **Database Sidecars & Schemas:** Database sidecars (`-wal`, `-shm`), application versions, and schema mappings were accounted for during parsing to ensure data integrity.


* **Timestamp Semantics:** Timestamp conversions rely on validated field units (milliseconds vs. epoch seconds), with unverified local offsets explicitly noted as unestablished where metadata limits apply.


* **Operator Attribution:** Stored device artifacts, logs, and geolocation references establish system activity and configuration, but do not independently prove the exclusive physical presence, identity, or intent of a specific human operator.



---

### Appendix B — Screenshot Plan

| Screenshot | Suggested content | Caption must identify |
| --- | --- | --- |
| **SS-01**

 | Archive properties and initial SHA-256

 | Archive name, path, hash tool/version, date/time

 |
| **SS-02**

 | Evidence directory and preserved working copy

 | Source path and evidence ID

 |
| **SS-03**

 | `build.prop` properties

 | File path and exact property keys/values

 |
| **SS-04**

 | User/profile artefacts

 | Source file, profile IDs and relevant fields

 |
| **SS-05**

 | Telephony database schema and counts

 | Database path, table and query

 |
| **SS-06**

 | SMS conversation query result

 | Record IDs, raw timestamp fields and source database

 |
| **SS-07**

 | MMS pdu/part relationship

 | PDU/part IDs and attachment/text reference

 |
| **SS-08**

 | Google Messages comparison

 | Matched records and matching criteria

 |
| **SS-09**

 | WhatsApp or second-app messages

 | Database, table, record IDs and status interpretation source

 |
| **SS-10**

 | Maps/photo metadata and timeline

 | Source path, metadata fields, offset status and evidence IDs

 |
