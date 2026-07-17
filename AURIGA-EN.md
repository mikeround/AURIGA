<div align="center">

<h1>AURIGA</h1>

<h2>MASTER PROMPT</h2>

<p><strong>Complete specification for building a personal tool equivalent to AURIGA-PERSONAL 2.1.0</strong></p>

<p>
  <img alt="Version 1.0" src="https://img.shields.io/badge/version-1.0-08796F?style=flat-square">
  <img alt="Personal use" src="https://img.shields.io/badge/use-personal-071521?style=flat-square">
  <img alt="English language" src="https://img.shields.io/badge/language-EN-647582?style=flat-square">
  <img alt="Local-first architecture" src="https://img.shields.io/badge/architecture-local--first-C78316?style=flat-square">
</p>

</div>

---

| Document | Details |
| --- | --- |
| **Version** | 1.0 |
| **Intended use** | Personal use, local-first, distributable as an unsigned portable package |
| **Application languages** | Spanish and English |
| **Document language** | Technical English |
| **Date** | 2026-07-17 |

> [!IMPORTANT]
> Deliver this entire document to a software engineering agent with file-system access and permission to run tests. The agent must not stop at a mock-up: it must implement, verify, package, and return an operational application.

> [!WARNING]
> Classification: personal use. The absence of code signing does not remove the internal requirements for encryption, integrity, auditability, backups, or access control.

---

## Table of contents

1. [How to use this document](#1-how-to-use-this-document)
2. [Copyable master prompt](#2-copyable-master-prompt)
3. [Reference architecture](#3-reference-architecture)
4. [Essential data contracts](#4-essential-data-contracts)
5. [Recommended local API](#5-recommended-local-api)
6. [Configuration and secrets](#6-configuration-and-secrets)
7. [Step-by-step implementation plan](#7-step-by-step-implementation-plan)
8. [Mandatory tests](#8-mandatory-tests)
9. [Final acceptance matrix](#9-final-acceptance-matrix)
10. [Unsigned personal packaging](#10-unsigned-personal-packaging)
11. [Residual risks](#11-residual-risks-that-must-be-disclosed)
12. [Required final implementation report](#12-final-report-required-from-the-engineering-agent)
13. [Recommended next improvements](#13-recommended-next-improvements)

---

## 1. How to use this document

Copy everything from section 2 through the `END OF MASTER PROMPT` marker and provide it to an engineering agent. If an earlier AURIGA release or its repository exists, attach it so that the agent can preserve compatible architecture, data flows, and case-file formats. The agent must work in verifiable phases, maintain a decision log, and must not declare completion until every acceptance criterion has passed.

- Grant write access only to an authorized working directory and the final delivery directory.
- Do not include real API keys in the prompt or repository. Configure them later through the encrypted vault.
- Require a backup before migrating data from any previous release.
- Require test evidence: successful builds, automated test results, startup from a clean ZIP extraction, hashes, and diagnostics.
- For personal use, use the portable launcher. Reserve code signing for professional or third-party distribution.

> [!IMPORTANT]
> Expected result: an operational local-first application, not a visual demonstration or an untested collection of files.

## 2. COPYABLE MASTER PROMPT

> [!IMPORTANT]
> START OF MASTER PROMPT

### ROLE AND DELIVERY METHOD

> Act as a senior engineering team comprising a software architect, security engineer, multimedia specialist, AI engineer, bilingual UX designer, QA engineer, and Windows release engineer.
>
> Build a new application named AURIGA-PERSONAL for personal use, equivalent or superior to AURIGA-PERSONAL 2.1.0. It must be a real, robust, portable, local-first, operational application, not a mock-up.
>
> Work autonomously inside the authorized directory. Inspect any existing source code or previous release first. Preserve everything that works, especially the architecture, data flow, case-file formats, and security controls. Document every incompatibility.
>
> Divide the work into verifiable phases. Run checks proportionate to the risk after every material change. Do not declare the project complete while any build, startup, dependency, critical security, or data-loss defect remains.

### PRODUCT OBJECTIVE

> AURIGA-PERSONAL must organize cases, ingest large volumes of evidence and data, retain encrypted originals, extract deterministic information, request structured assessments from AI models, support human review, and generate professional case files in PDF and other requested formats.
>
> It must handle images, audio, video, PDF, plain text, CSV, TSV, JSON, JSONL, XML, HTML, Markdown, RTF, logs, source code, office documents, and arbitrary binary files. When no native extractor exists, retain, catalog, hash, and seal the file while clearly reporting the limitation. Never claim to have interpreted unsupported content.
>
> It must support authorized real-time capture from local cameras and microphones. Devices must be off by default, require explicit permission, and display a persistent indicator while active.

### NON-NEGOTIABLE REQUIREMENTS

> Provide a complete Spanish and English interface with a visible language selector and persistent preference. Reports and case files must also support both languages.
>
> Support multiple-file upload. The default per-file limit is 4 GB and must be configurable. Never load complete large files into memory.
>
> Calculate SHA-256 incrementally over the original file before final case ingestion.
>
> Use chunked authenticated AES-256-GCM encryption. Cryptographically bind each chunk to the header, index, length, and ordering so that substitution, reordering, truncation, and alteration are detected.
>
> Retain read compatibility with evidence from the previous release. Migrations must be atomic, recoverable, and preceded by a backup.
>
> Serve audio and video over HTTP Range requests without decrypting the entire file into memory.
>
> Keep upload and processing temporary files in separate directories. Perform best-effort secure cleanup after both success and failure.
>
> Encrypt the database, audit trail, metrics, secrets vault, signing key, and stored evidence at rest.
>
> Protect the master key with Windows DPAPI CurrentUser. On other platforms, require a master passphrase derived with scrypt or Argon2id.
>
> Never log or return API keys, tokens, passwords, or sensitive file contents in error messages.
>
> Bind the application to `127.0.0.1` by default. Apply security headers, CSP, rate limits, strict validation, and administrator, analyst, and read-only roles.
>
> Never execute ingested files, open them as code, or serve them with an executable MIME type. Treat every ingested item as untrusted content.

### REAL-TIME CAPTURE AND PROCESSING

> Provide camera, microphone, and combined camera-plus-microphone modes through MediaDevices and MediaRecorder, or an equivalent technology.
>
> Support configurable 10, 30, 60, and 300-second segments. Every segment must be an independently playable file, not a headerless media fragment.
>
> When closing a segment, calculate its hash, encrypt it, register chain-of-custody information, extract metadata, and update the case.
>
> Automated AI assessment must be optional and disabled by default. Before activation, warn that data may be sent to third parties and may incur charges.
>
> Allow capture to stop immediately, close every media track, and display the real device state. Also stop tracks when the component is left or the case is closed.
>
> For sustained capture, use a bounded-concurrency queue with backpressure. If analysis falls behind, continue sealing segments and display pending work without losing data.

### AI PROVIDERS

> Implement separate adapters for Google Gemini, OpenAI/ChatGPT, Anthropic Claude - including Fable, Opus, Sonnet, and Haiku when available to the account - xAI Grok, Alibaba Qwen, DeepSeek, local Ollama, and an OpenAI-compatible gateway.
>
> Configure keys through an encrypted vault and never send them to the browser. Ollama must operate without a key on `127.0.0.1` and discover installed models.
>
> Do not hard-code business logic to model names that will expire. Maintain updateable suggested catalogs, an editable model field, and model discovery wherever the provider supports it.
>
> Declare capabilities per provider: text, image, audio, video, and PDF. Reject unsupported combinations with a clear, actionable explanation.
>
> Do not send multi-gigabyte files as base64. Define `MAX_INLINE_AI_MB`; above that limit, extract context, segment, sample, or request a reproducible user selection.
>
> Validate every model response against a strict schema before persistence. Record provider, model, timestamp, duration, token usage, estimated cost, schema version, and limitations.
>
> Use exponential backoff only for transient failures. Do not automatically retry authorization, validation, or payload-size errors.
>
> Offer consensus across two to six models and display agreement, disagreement, failed runs, and cost. Never present model consensus as a proven fact.

### ANALYSIS AND UTILITIES

> Provide multimodal general, security, integrity, comparison, audio, agriculture, and observable health-signal protocols. The health protocol must not diagnose disease.
>
> Perform deterministic extraction using EXIF, ffprobe, music-metadata, file size, actual MIME type, duration, streams, codecs, resolution, sample rate, text, and basic structure.
>
> Provide local OCR with Tesseract for images. Perform bounded text extraction for text, CSV, JSON, XML, HTML, RTF, and logs, explicitly marking truncated samples.
>
> Support non-destructive physical segmentation of audio and video with FFmpeg. Add every output as derived evidence referencing the original item and time range.
>
> Run batch processing in the background with a job identifier, state, totals, completed and failed counts, per-item results, and configurable concurrency from one to four workers.
>
> Add pagination and search for cases containing thousands of evidence items. Avoid giant JSON responses and avoid `Promise.all` across every original file.

### CASE FILES AND OUTPUTS

> Generate a professional PDF containing a cover, case identification, methodological notice, evidence inventory, hashes, results, human reviews, limitations, and chained audit trail.
>
> Also export self-contained printable HTML, Markdown, TXT, structured JSON, CSV, and a signed ZIP containing originals decrypted through streaming.
>
> Sign manifests and human reviews with Ed25519. Encrypt the private key. Include the public-key fingerprint and enough information for verification outside AURIGA.
>
> Provide a locally sealed, read-only best-effort copy and explain that it is neither WORM storage nor an RFC 3161 timestamp.
>
> Provide optional signed webhooks for SIEM, VMS, and eDiscovery. Enforce an allowlist of destinations and do not follow redirects into unauthorized networks.

### USER EXPERIENCE

> Build an intuitive, restrained, accessible interface adaptable to desktop and mobile. Use comprehensible loading and error states without unnecessary jargon.
>
> Include a case dashboard, evidence inventory, multimedia viewer, analysis configuration, deterministic utilities, history, analysis-restricted chat, and signed human review.
>
> Always state that AI conclusions are screening observations. Do not perform facial identification, medical diagnosis, sensitive-attribute inference, or attribution of guilt.
>
> Do not block the browser while loading large files. Display progress, queue state, size, short hash, detected type, date, and processing status.
>
> An inactive camera preview must explicitly say that the camera is off. Do not show a black screen that users could mistake for a failure.

### QUALITY, SECURITY, AND DELIVERY

> Apply strict TypeScript, Zod or equivalent runtime validation, centralized error handling, and clear separation between client, API, domain, storage, security, providers, and export layers.
>
> Create unit, integration, security, streaming, range, encryption, header-tampering, audit, role, migration, and response-schema tests.
>
> Run tests with large synthetic files and demonstrate bounded memory consumption.
>
> Generate a CycloneDX SBOM, production-dependency audit, threat model, and documentation for operations, compatibility, backups, restoration, and incident response.
>
> Build a self-contained Windows x64 package containing a portable Node runtime and physical dependencies, with no junctions, symbolic links, or reparse points.
>
> The personal edition must start through `INICIAR_AURIGA_PERSONAL.cmd` without installation, signature, certificate, or administrator privileges. Keep the console open and launch `http://127.0.0.1:4174`.
>
> Create a JSON manifest and SHA-256 file beside the ZIP. Extract the ZIP into a clean directory and start it successfully before delivery.
>
> Preserve `data` and `.env` during upgrades. Never overwrite or delete them when deploying a new release.

### MANDATORY DELIVERABLES

> Deliver complete source code, a production build, portable runtime, production dependencies, tests, and documentation.
>
> Deliver an operational `AURIGA` directory and `AURIGA-PERSONAL-<version>.zip` for personal use.
>
> Include `INICIAR_AURIGA_PERSONAL.cmd`, `CONFIGURAR_CLAVES.cmd`, `DIAGNOSTICO.cmd`, `CREAR_COPIA.cmd`, and `RESTAURAR_COPIA.cmd`.
>
> Include README, CHANGELOG, SECURITY, threat model, architecture, operations, AI evaluation, and optional signing guide documents.
>
> Return a final report containing the version, locations, SHA-256 values, passed tests, residual risks, and exact startup instructions.

### COMPLETION CONDITION

> Confirm completion only when the project builds without errors; all tests pass; the installed directory starts; a clean ZIP extraction starts; the health endpoint reports the correct version; the audit chain is valid; the large-file limit is effective; capture is off by default; Spanish and English work; and every published hash matches.
>
> If a dependency is missing, a native binary is absent, the ZIP loses transitive dependencies, or the application fails to listen on its port, correct the problem, repackage, and repeat the entire final validation.

> [!IMPORTANT]
> END OF MASTER PROMPT

## 3. Reference architecture

The recommended architecture keeps the browser as an unprivileged client and concentrates secrets, encryption, provider access, and file operations in the local server. No API key may be embedded in the client bundle.

```text
React/TypeScript browser client
  |-- Spanish/English UI
  |-- multiple upload and MediaDevices/MediaRecorder capture
  |-- viewer using Range requests
  |-- job and result dashboard
  v
Express API on 127.0.0.1
  |-- authentication and roles
  |-- Zod validation and rate limiting
  |-- case, evidence, analysis, and export services
  |-- bounded-concurrency job queue
  +--> Encrypted local storage
  |      |-- database.enc / audit.enc / metrics.enc
  |      |-- cases/<caseId>/<evidenceId>.auriga
  |      +-- vault and DPAPI-protected keys
  +--> Local utilities
  |      |-- FFmpeg / ffprobe
  |      |-- EXIF / music-metadata
  |      +-- Tesseract OCR
  +--> AI adapters
         |-- Gemini / OpenAI / Anthropic / xAI
         |-- Qwen / DeepSeek
         |-- Ollama
         +-- OpenAI-compatible gateway
```

### 3.1 File-ingestion flow

- Multer or an equivalent component writes to `upload-temp` using a random name and configurable limit.
- Detect file type from content whenever possible. Use the extension only as a hint, never as sufficient proof.
- Calculate SHA-256 by reading the file sequentially.
- Encrypt in chunks into a temporary file inside the destination directory.
- Synchronize and atomically rename the encrypted file; only then register the evidence and audit event.
- Delete the uploaded temporary file in a `finally` block. If registration fails, remove the orphaned encrypted file.

### 3.2 Chunked encrypted format

A straightforward, verifiable implementation can use the following structure. Authenticate the header and ordering fields as Additional Authenticated Data for every chunk.

```text
Header:
  magic[8]             = AURIGA3\0
  chunk_size_uint32    = 4 MiB by default
  plaintext_size_u64   = total original size

For each chunk:
  plaintext_len_u32
  iv[12]               = random and unique
  tag[16]
  ciphertext[n]

AAD for each chunk:
  complete header + index_u64 + plaintext_len_u32
```

> [!WARNING]
> Never reuse an IV. Reject absurd lengths, truncated files, invalid authentication tags, and decrypted text exceeding the configured limit. Delete every partial output after an error.

### 3.3 Proposed directory structure

```text
AURIGA/
  dist-client/                 compiled client
  dist-server/                 compiled API
  runtime/node.exe             portable runtime
  node_modules/                physical production dependencies
  data/                        never included in upgrades
    cases/<caseId>/
    upload-temp/
    temp/
    database.enc
    audit.enc
    master-key.dpapi
    secrets.vault
  src/                         user interface
  server/                      API and services
  shared/                      shared schemas
  tests/                       test suites
  docs/                        architecture, threats, and operations
  INICIAR_AURIGA_PERSONAL.cmd
  CONFIGURAR_CLAVES.cmd
  DIAGNOSTICO.cmd
  CREAR_COPIA.cmd
  RESTAURAR_COPIA.cmd
```

## 4. Essential data contracts

### 4.1 Evidence

```text
EvidenceRecord {
  id: UUID
  caseId: UUID
  originalName: string <= 255
  storedName: string
  mimeType: string
  size: positive integer
  sha256: 64 hex characters
  label: string
  capturedAt: ISO datetime | null
  ingestedAt: ISO datetime
  derivedFromEvidenceId?: UUID | null
  enrichment?: {
    extractedAt: ISO datetime
    technical: object
    extractedText: string <= configured cap
    language: string
    truncated?: boolean
  }
}
```

### 4.2 Analysis result

- Summary and observations with confidence, nullable timestamp, and a visual, audio, metadata, or multimodal basis.
- Objects or entities with label, state, attributes, confidence, and a normalized `0..1000` bounding box where applicable.
- Events with category, severity, confidence, time, and observation.
- Audio results containing language, transcript excerpt, sound events, and notes.
- Integrity screening using `consistent`, `suspicious`, or `inconclusive`, always with a methodological warning.
- Reproducible comparison against reference evidence, nullable similarity, differences, and a limited conclusion.
- Contextual risk and audiovisual-coherence assessment.
- A non-empty list of limitations.

### 4.3 Chained audit trail

```text
AuditEntry {
  sequence: monotonically increasing integer
  id: UUID
  timestamp: ISO datetime
  action: string
  caseId: UUID | null
  evidenceId: UUID | null
  details: object containing no secrets
  previousHash: SHA-256 or GENESIS
  hash: SHA-256(canonical JSON of every preceding field)
}
```

Verification must traverse the complete chain and return `valid`, the entry count, and the first invalid sequence. At larger scale, evolve toward segmented append-only logs without breaking verifier compatibility.

## 5. Recommended local API

| Method | Route | Purpose |
| --- | --- | --- |
| GET | `/api/health` | Version, capabilities, providers, limits, and audit status |
| GET/POST | `/api/cases` | List and create cases |
| GET/DELETE | `/api/cases/:caseId` | Retrieve or delete a case with confirmation |
| POST | `/api/cases/:caseId/evidence` | Ingest a file through streaming |
| GET | `/api/cases/:caseId/evidence/:id/content` | Decrypted content with Range support |
| POST | `/api/cases/:caseId/evidence/:id/enrich` | Metadata, text, and OCR enrichment |
| POST | `/api/cases/:caseId/evidence/:id/segment` | Create a physical derived segment |
| POST | `/api/cases/:caseId/evidence/:id/analyze` | Analyze with a selected provider and model |
| POST | `/api/cases/:caseId/evidence/:id/consensus` | Run multi-model consensus |
| POST | `/api/cases/:caseId/batch/enrich` | Start a background batch job |
| GET | `/api/jobs/:jobId` | Retrieve job state and progress |
| POST | `/api/cases/:caseId/analyses/:id/review` | Add an Ed25519-signed human review |
| GET | `/api/cases/:caseId/report.pdf` | Generate a Spanish or English PDF case file |
| GET | `/api/cases/:caseId/document.:format` | Generate HTML, Markdown, TXT, JSON, or CSV |
| GET | `/api/cases/:caseId/export.zip` | Export a signed package containing originals |
| GET | `/api/cases/:caseId/audit` | Retrieve and verify the audit trail |

## 6. Configuration and secrets

| Variable | Initial value | Purpose |
| --- | --- | --- |
| `PORT` | `4174` | Local listening port |
| `MAX_UPLOAD_MB` | `4096` | Per-file limit |
| `MAX_INLINE_AI_MB` | `25` | Direct AI-submission limit |
| `ENCRYPTION_CHUNK_MB` | `4` | AES-GCM chunk size |
| `*_API_KEY` | empty | Migrate immediately into the encrypted vault |
| `*_MODEL` | editable | Suggested model for each provider |
| `OLLAMA_BASE_URL` | `127.0.0.1:11434` | Local Ollama server |
| `AURIGA_ACCESS_TOKEN` | generated | Administrator access |
| `AURIGA_ANALYST_TOKEN` | optional | Analyst access |
| `AURIGA_VIEWER_TOKEN` | optional | Read-only access |
| `AURIGA_DATA_DIR` | `./data` | Encrypted storage location |

> [!WARNING]
> Do not display configured secrets in the interface, even partially masked. Allow users to replace or delete them. Protect the vault with the same master key and authenticate its complete contents.

## 7. Step-by-step implementation plan

### Phase 0 - Discovery and backup

Inventory the repository, dependencies, data formats, and flows. Create a verifiable backup. Document risks and do not modify real data during development.

### Phase 1 - Skeleton and contracts

Create the client, API, shared schemas, configuration, error handling, and basic tests. Establish the version and release structure.

### Phase 2 - Secure custody

Implement DPAPI or master-passphrase protection, the secrets vault, atomic encryption, chunked streaming, hashes, audit trail, and backward-compatible reading.

### Phase 3 - High-volume ingestion

Implement disk-based upload, multiple selection, broad type support, limits, temporary-file handling, progress, Range requests, and memory tests.

### Phase 4 - Metadata and media

Integrate ffprobe, FFmpeg, EXIF, music-metadata, text extraction, OCR, and derived evidence.

### Phase 5 - Real-time operation

Implement permissions, preview, MediaRecorder, independently playable segments, queues, backpressure, sealing, and reliable device shutdown.

### Phase 6 - AI adapters

Implement the common interface, capability declarations, editable models, cloud providers, Ollama, response validation, retries, usage, and cost reporting.

### Phase 7 - Batches and consensus

Create persistable jobs, progress reporting, per-item errors, bounded concurrency, and multi-model consensus.

### Phase 8 - Bilingual interface

Translate every state, form, modal, error, help view, accessibility label, and date format. Test desktop and mobile layouts.

### Phase 9 - Reports and signatures

Implement professional PDF, HTML, Markdown, TXT, JSON, CSV, streaming ZIP, Ed25519 manifest signatures, and signed human reviews.

### Phase 10 - Distributable product

Create startup scripts, optional installation, conservative upgrades, backup, restoration, diagnostics, SBOM, and operational documentation.

### Phase 11 - Security and quality

Run test suites, production dependency audits, tampering tests, role tests, limit tests, partial-failure tests, migrations, AI evaluation, and threat analysis.

### Phase 12 - Clean validation

Package physical dependencies, verify binaries, confirm zero reparse points, extract a clean ZIP, start it, verify health, and publish hashes.

## 8. Mandatory tests

| Area | Test | Pass criterion |
| --- | --- | --- |
| Encryption | Round-trip a file spanning multiple chunks | Content and SHA-256 are identical |
| Encryption | Alter header, order, tag, or ciphertext | Decryption is rejected and no temporary file remains |
| Streaming | Process a large synthetic file | Memory remains bounded; no full-file Buffer exists |
| Range | Request an intermediate byte range | Status 206, correct Content-Range, and exact bytes |
| Upload | Ingest an unknown type | Retained as octet-stream and never executed |
| Upload | Exceed the configured limit | Clear 413 response and temporary file removed |
| Audit | Modify an audit entry | Chain becomes invalid and the sequence is identified |
| Roles | Viewer attempts POST or DELETE | Status 403 |
| AI | Provider returns an invalid schema | Result is not persisted; controlled error returned |
| AI | File exceeds `MAX_INLINE_AI_MB` | Segment, summarize, or reject with actionable guidance |
| Real time | Start and stop capture | Permission, indicator, segments, and closed tracks verified |
| Real time | Analysis runs slower than capture | Queue remains visible and no segment is lost |
| Export | Export a case with large evidence | Streaming ZIP and verifiable manifest |
| Bilingual | Complete Spanish and English workflows | No unintended residual text from the other language |
| Upgrade | Install over existing data | `data` and `.env` remain intact |
| Portability | Extract a clean ZIP | Starts without installing Node or dependencies |
| Dependencies | Search for reparse points and `ip-address` | Zero links and all transitive dependencies present |

## 9. Final acceptance matrix

- [ ] **01.** UI, health, diagnostics, `package.json`, and manifests report the same version.
- [ ] **02.** Every newly ingested original is stored in authenticated chunked encrypted format.
- [ ] **03.** Multiple files and a file larger than 20 MB can be ingested without exhausting memory.
- [ ] **04.** The effective default limit is 4 GB unless explicitly configured otherwise.
- [ ] **05.** Audio and video support playback and temporal seeking through Range requests.
- [ ] **06.** Camera and microphone are off by default, require permission, and display an active indicator.
- [ ] **07.** Every live segment is independent, sealed, and recorded in the audit trail.
- [ ] **08.** All eight provider adapters exist and Ollama discovers local models.
- [ ] **09.** Model names are editable and keys remain exclusively on the server or in the vault.
- [ ] **10.** Main interface, dialogs, errors, reports, and exports operate in Spanish and English.
- [ ] **11.** PDF, HTML, Markdown, TXT, JSON, CSV, and ZIP outputs generate without errors.
- [ ] **12.** Signed ZIP generation does not load all evidence into memory simultaneously.
- [ ] **13.** Automated tests and the production build exit with code 0.
- [ ] **14.** The production dependency audit contains no undocumented known critical vulnerability.
- [ ] **15.** The portable package contains the runtime, multimedia binaries, and physical dependencies without links.
- [ ] **16.** A clean extraction starts and returns a correct health response.
- [ ] **17.** The personal launcher works without signature, certificate, or administrator privileges.
- [ ] **18.** Upgrades preserve `data` and `.env`.
- [ ] **19.** SHA-256 values and a manifest are published for every ZIP.
- [ ] **20.** Residual risks and limitations are documented, and AI is not presented as a conclusive forensic examination.

## 10. Unsigned personal packaging

For personal use, the application may be delivered without code signing. The package must be self-contained, but it must never attempt to disable SmartScreen, Smart App Control, antivirus protection, UAC, or organizational policies.

```bat
INICIAR_AURIGA_PERSONAL.cmd

@echo off
setlocal EnableExtensions
cd /d "%~dp0"
title AURIGA - Personal edition
if not exist "runtime\node.exe" (
  echo [ERROR] runtime\node.exe is missing
  pause
  exit /b 1
)
if not exist "data" mkdir "data"
start "" "http://127.0.0.1:4174"
"runtime\node.exe" --enable-source-maps dist-server\server\index.js
if errorlevel 1 pause
endlocal
```

- The personal ZIP may also contain installation scripts, but the recommended workflow uses the portable launcher.
- Include `USO_PERSONAL_SIN_FIRMA.txt` with startup, key configuration, backups, integrity, and limitation instructions.
- The absence of a signature does not reduce encryption or internal auditability; it only prevents public verification of the software publisher.
- For third-party distribution, sign executables and the installer with a recognized certificate or signing service and an RFC 3161 timestamp.

## 11. Residual risks that must be disclosed

- DPAPI protects against offline disk copying, not against malware controlling the user's active session.
- Overwriting data on SSD storage is best effort. Strict destruction requires volume encryption and destruction of encryption keys.
- A read-only file is neither WORM storage nor certified custody.
- AI assessments can be incomplete or incorrect and require qualified human review.
- Generative integrity or deepfake screening does not replace specialized forensic measurement.
- Provider limits and formats change. The application must degrade safely and retain configurable model names.
- A completely encrypted JSON database may be adequate for personal use, but deployments containing millions of records require an indexed, paginated, encrypted transactional database.
- Office-document analysis depends on available extractors. Retention does not imply interpretation.

## 12. Final report required from the engineering agent

```text
1. Result: final version and operational status.
2. Installed-directory and personal-ZIP locations.
3. SHA-256 for every package.
4. Implemented functions and deliberately limited functions.
5. Tests executed and exact results.
6. Verification from a clean extraction.
7. Dependency-audit and SBOM status.
8. Personal-use startup procedure.
9. Cloud-key and Ollama configuration procedure.
10. Backup, restoration, and migration procedure.
11. Residual risks and recommended future work.
```

## 13. Recommended next improvements

- Use an encrypted, paginated transactional database for hundreds of thousands or millions of evidence records.
- Add persistent workers with restart recovery and per-case priorities.
- Add local Whisper-compatible audio transcription and optional non-identifying speaker diarization.
- Add sandboxed extraction for DOCX, XLSX, PPTX, ODF, and PDF with ZIP-bomb limits.
- Add reproducible long-video sampling with scene index, thumbnails, and temporal map.
- Add optional RFC 3161 sealing and external WORM storage.
- Add signed proprietary connectors for specific VMS, SIEM, and eDiscovery systems.
- Add updates verified through a signed manifest with automatic rollback.
- Add reproducible provider/model evaluations using reference datasets and regression thresholds.

---

> [!IMPORTANT]
> END OF DOCUMENT - AURIGA MASTER PROMPT
