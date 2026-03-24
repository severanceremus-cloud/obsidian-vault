# ts3-listener

**Status:** ✅ Abgeschlossen (aktiv im Einsatz)
**Repo:** https://github.com/scrato/ts-listener
**Zuletzt aktualisiert:** 2026-03-24

## Was ist das?

Python-basierter TS3-Bot der P&P-Sessions aufzeichnet und transkribiert. Nutzt `faster-whisper` (Modell: `large-v3`) für Deutsch-Transkription. Output als `.txt`-Datei für [[myarchivist]].

## Architektur

```
TS3 Client → Virtuelles Audio-Device → audio_capture.py (VAD) → whisper_transcriber.py → FastAPI REST + SSE
                                                                       ↑
                                                                ts3_bot.py (ServerQuery, Sprecher-Erkennung)
```

## Output-Format

```
[00:01:23] <Spielleiter>: Ihr steht vor dem alten Turm.
[00:01:27] <Krieger>: Ich ziehe mein Schwert.
```

Dateien: `data/transcriptions/YYYY-MM-DD_HH-MM.txt`

## Wichtige Einstellungen

- Sprache: `de` (fest)
- Initial prompt: *"Dies ist ein Pen and Paper Rollenspiel auf Deutsch."*
- VAD: 1.5s Stille-Toleranz (für deutsche Komposita)
- `beam_size=5` für komplexe deutsche Wörter

## API

| Endpoint | Beschreibung |
|----------|-------------|
| `POST /session/start` | Session starten |
| `GET /transcriptions` | Alle Transkriptionen |
| `GET /transcriptions/live` | SSE Live-Stream |
| `GET /clients` | Verbundene TS3-Clients |

## PRs (merged)

- [PR #1](https://github.com/scrato/ts-listener/pull/1) — Initial TS3 Transcription Bot
- [PR #2](https://github.com/scrato/ts-listener/pull/2) — German Audio Optimization + .txt Output

## Verknüpfungen

- [[myarchivist]] — konsumiert die `.txt`-Output-Dateien
- [[abs-wear]] — unabhängiges Projekt

## Notizen

- Audio-Setup: PipeWire Null-Sink (`ts3-sink.monitor`) empfohlen für Linux
- GPU-Empfehlung: NVIDIA für `large-v3` mit `compute_type=float16`
