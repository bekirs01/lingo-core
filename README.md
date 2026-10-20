# Lingo Core

Premium offline language-learning app family core. One engine, multiple target languages, no account required.

This repository is the **master template**. Clone it for a Spanish, Japanese, Korean, or other language product. Do not rewrite Dart screens or the engine for a new language.

## Technology

Flutter and Dart. iOS-first, Android compatible. Offline-first. No backend, Firebase, Supabase, authentication, ads, or analytics.

## Run

```bash
flutter pub get
flutter run
```

Then:

```bash
dart format .
flutter analyze
flutter test
```

## Clone a language product

1. Copy this project.
2. Replace `assets/product.json` (display name, target language, direction, writing system, accent, translation languages, feature flags).
3. Replace `assets/content/` (language pack, alphabet, words, phrases, learner translations).
4. Reuse or replace category / alphabet / paper images. Missing PNGs fall back to painted art.
5. Optional: add spoken audio under `assets/audio/` and point content rows at those files. Native TTS speaks the target language when a recording is absent. `featureFlags.audio` hides speakers when false.
6. Later, in the **cloned** iOS/Android projects, set the store name, icon, logo, bundle ID, screenshots, and metadata. Do not treat this master as a finished App Store listing.

See `docs/LANGUAGE_PACK_GUIDE.md` for the field-by-field pack format.

## How the layers fit

| Layer | Where | What it does |
| --- | --- | --- |
| Product identity | `assets/product.json` | Name, accent, writing system, direction, translation languages, `alphabet` / `audio` flags |
| Target-language content | `assets/content/*.json` | Glyphs, words, phrases, optional romanization and audio IDs |
| Learner meanings | `assets/content/translations/<code>.json` | Gloss of each content ID in the learner's language |
| UI chrome | `lib/core/l10n/` | Nav, settings, quiz, empty states. English and Turkish ship in the catalog; clones may overlay keys |

Switching Translation Language changes learner glosses and UI chrome. It never replaces the target-language `text` / `glyph`.

## Feature flags

- `alphabet`: when false (or `writingSystem` is `other`), the Alphabet tab stays but shows an empty inventory.
- `audio`: when true, play controls speak the target language (bundled recording if present, otherwise native TTS). UI sound effects are separate and gated by Settings.

Romanization is not a flag. If a row has a `romanization` value distinct from `pronunciation`, Alphabet shows it.

## Quiz

Words, phrases, and alphabet units with `quizEnabled: true` feed the in-app Quiz. Launch a mixed session from Home, or a words/phrases session from those tabs. Alphabet items only use recognition modes. Eligibility rules live in the language-pack guide.

## Product-specific branding later

Keep this master generic. App icon, logo, final display name, bundle ID, screenshots, store description, and keywords belong to each cloned product.

## Principles

- English-only code, comments, docs, identifiers, and base UI copy
- Modular, reusable architecture; data-driven learning content
- Small widgets, no duplicated business logic, `const` where it belongs
- Premium UI with motion, depth, sound, and haptics that stay fast and accessible
- No extra packages or architecture changes without an explicit reason
