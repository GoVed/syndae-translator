# Universal Multi-Language Translator Tool Instructions

## Overview
The **Translator Tool** (`translate`) is an open, generic translation and localization service for Syndae Agent OS. It is designed to serve operators and users globally across **50+ languages**, formal & colloquial communication styles, and customized regional dialects:

1. **Global Languages**: English, Spanish, French, German, Chinese (Simplified/Traditional), Japanese, Korean, Arabic, Russian, Portuguese, Italian, Dutch, Hindi, Bengali, etc.
2. **Colloquial & Transliterated Dialects**:
   - `gujlish`: Conversational Gujarati written phonetically in the Latin/English alphabet (common for WhatsApp & SMS).
   - `hinglish`: Conversational Hindi written phonetically in the Latin alphabet.
   - `romaji` / `pinyin`: Romanized Japanese and Chinese.
3. **Regional Native Scripts**: Native Gujarati script (ગુજરાતી), Devanagari Hindi (हिन्दी), Kanji/Kana (日本語), Arabic script (العربية), etc.

---

## Translation Guidelines

The **`translate`** tool provides high-fidelity, culturally nuanced translation, transliteration, and sociolinguistic localization across languages and colloquial dialects.

1. **Autonomous Translation Capability**:
   - Advanced multi-lingual models may translate directly when capable.
   - When precision, transliteration (e.g. phonetic Gujlish / Hinglish), dialect nuances, or specific honorifics are required, invoke `translate` to ensure accurate and authentic communication.
2. **Dialect and Transliteration Support**:
   - Regional conversational dialects (such as Gujlish, Hinglish, Romaji) often benefit from the tool's specialized dictionary and pronunciation rules.
3. **Outbound Messaging**:
   - When communicating with external contacts on messaging channels (e.g. WhatsApp, Email), verify or translate the message into the recipient's preferred language or dialect.
4. **Tone and Formality Matching**:
   - Use `tone: "casual"` for chat platforms.
   - Use `tone: "formal"` or `tone: "business"` for professional correspondence.
   - Provide `context` (e.g., `formality: "respectful"`, `relationship: "elder"`) whenever respect tiers or gender agreements matter.

---

## Tool Signature

```json
{
  "name": "translate",
  "arguments": {
    "text": "Hello, thank you for reaching out. How can I assist you today?",
    "target_lang": "spanish",
    "source_lang": "auto",
    "tone": "formal"
  }
}
```

### Parameters
- **`text`** *(string, required)*: The text string to translate.
- **`target_lang`** *(string, required)*: Target language code or name (e.g., `"spanish"`, `"french"`, `"german"`, `"gujlish"`, `"gujarati"`, `"hindi"`, `"japanese"`, `"chinese"`, `"arabic"`, etc.).
- **`source_lang`** *(string, optional, default: `"auto"`)*: Source language or `"auto"` for automatic detection.
- **`tone`** *(string, optional, default: `"natural"`)*:
  - `"natural"`: Standard conversational translation.
  - `"casual"`: Friendly, informal chat style.
  - `"formal"`: Respectful and polite grammar.
  - `"business"`: Professional enterprise terminology.
  - `"slang"`: Colloquial slang.
- **`glossary`** *(object, optional)*: Key-value terms to preserve or enforce verbatim (e.g., `{"Syndae": "Syndae", "Agent OS": "Agent OS"}`).
- **`context`** *(object or string, optional)*: Sociolinguistic and cultural context. Unlike English, foreign languages change grammar, pronouns, and verb conjugations based on honorifics and gender:
  - `formality` *(string)*: `"respectful"` / `"formal"` / `"honorific"` (use `tame` in Gujarati, `aap` in Hindi, `vous` in French, `Usted` in Spanish, `Sie` in German) vs `"casual"` / `"informal"` / `"peer"` (use `tu` / `tum` / `du`).
  - `recipient_gender` *(string)*: `"female"` or `"male"` (governs 2nd-person gendered verbs and adjectives).
  - `speaker_gender` *(string)*: `"female"` or `"male"` (governs 1st-person verb conjugations).
  - `relationship` *(string)*: Social dynamic, e.g. `"elder sister"`, `"mother"`, `"boss"`, `"client"`, `"close friend"`, `"younger brother"`.
  - `age_group` *(string)*: `"elder"`, `"peer"`, `"junior"`, `"child"`.
  - `additional_notes` *(string)*: Any situational nuance.

---

## Examples

### 1. English to Gujlish (Respectful Elder vs Casual Friend)
- **Input (Elder Uncle)**:
  `text: "Are you coming today?", target_lang: "gujlish", context: { formality: "respectful", relationship: "elder uncle", recipient_gender: "male" }`
  ➔ **Output**: `"Tame aaje aavsho?"`
- **Input (Casual Peer Friend)**:
  `text: "Are you coming today?", target_lang: "gujlish", context: { formality: "casual", relationship: "friend", recipient_gender: "female" }`
  ➔ **Output**: `"Tu aaje aavish?"`

### 2. English to Hinglish (Gender Agreement)
- **Input (Female Speaker to Male Colleague)**:
  `text: "I am working on it now, will let you know.", target_lang: "hinglish", context: { speaker_gender: "female", recipient_gender: "male", formality: "peer" }`
  ➔ **Output**: `"Main abhi ispar kaam kar rahi hoon, aapko bataoongi."`

### 3. English to Spanish (Formal Business vs Informal)
- **Input**: `text: "We appreciate your partnership. The contract is attached.", target_lang: "spanish", tone: "business", context: { formality: "formal" }`
- **Output**: `"Agradecemos su colaboración. El contrato se encuentra adjunto."`
