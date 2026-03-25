
# **Prompt for Building a Web-Based Rust/WASM Music Studio with Dioxus**

## **Project Overview**
Build a **web-based music studio** using **Rust, Dioxus, and WebAssembly (WASM)**. The app should run in the browser, support multi-track audio editing, MIDI, effects, and collaboration via P2P using Nostr.

The project should use a `.dioxmus` file format for storing everything from audio/MIDI tracks to settings, UI state, and metadata.

---

## **Core Requirements**

### **1. Project Management**
- **`.dioxmus` Project File**:
  - Store all project data in a single `.dioxmus` file (JSON/YAML/TOML format).
  - The file should contain:
    - Audio/MIDI tracks (with references to external files or embedded audio).
    - Plugin/effect chains (with parameters and automation).
    - UI state (window layout, theme, etc.).
    - Metadata (project name, author, BPM, time signature, etc.).
    - Versioning and backup support.

- **Project Templates**:
  - Provide built-in templates (e.g., "Empty Project", "Pop Beat", "EDM").

- **Automatic Saving**:
  - Auto-save every 30 seconds.
  - Manual save/load functionality.

---

### **2. Audio Engine**
- **Multi-Track Recording/Playback**:
  - Support for at least 8 audio tracks.
  - Non-destructive editing (undo/redo, clip splitting, time-stretching).
  - Real-time audio processing (filters, EQ, compression).

- **Audio File Support**:
  - Import/export: WAV, MP3, OGG, FLAC.
  - Audio bus routing (send/return tracks).

---

### **3. MIDI & Instruments**
- **MIDI File Support**:
  - Import/export MIDI files.

- **Virtual Piano Roll Editor**:
  - Note editing, velocity, automation.
  - On-screen piano keyboard for playing notes in different styles (e.g., grand piano, synth, electric piano).

- **MIDI Controller Support**:
  - Support for MIDI keyboards, pads, and controllers.
  - MIDI learn for custom controller mapping.

- **Built-in Synth**:
  - Subtractive synth with ADSR envelopes.

---

### **4. Effects & Plugins**
- **Built-in Effects**:
  - Reverb, delay, distortion, chorus, phaser, EQ.

- **Plugin System**:
  - Support for VST/AU plugins via WASM or Web Audio API.
  - Custom effect chain (drag-and-drop ordering).
  - Effect automation (draw curves in timeline).

---

### **5. UI/UX & Workflow**
- **Responsive UI**:
  - Customizable themes and layout presets.
  - Keyboard shortcuts (customizable).

- **Accessibility**:
  - Screen reader support.
  - High-contrast mode.
  - Keyboard-only navigation.

---

### **6. Collaboration**
- **Real-Time Collaboration**:
  - Use **Nostr (wss://nos.lol)** for peer discovery and P2P communication.
  - Support for multi-user editing in real-time.
  - Shareable project links (read-only or editable).

---

### **7. Export & Performance**
- **Export Mixdown**:
  - Export to WAV/MP3/OGG.

- **Performance**:
  - Low-latency audio processing (Web Audio API/WASM optimizations).
  - Background rendering for complex effects.

---

### **8. Extensibility**
- **Scripting Support**:
  - Lua scripting engine for custom tools and effects.
  - Open-source plugin SDK for community contributions.

---

## **Technical Stack**
- **Language**: Rust
- **Framework**: Dioxus (for UI)
- **WebAssembly**: WASM for browser compatibility
- **Audio Processing**: Web Audio API + Rust audio libraries (e.g., `cpal`, `fundsp`)
- **MIDI**: Web MIDI API + `midir` for Rust
- **Nostr**: P2P collaboration via `nostr-rs`
- **Scripting**: Lua via `mlua`

---

## **File Structure**
```
/dioxus-music-studio/
├── /src/
│   ├── main.rs          # Entry point
│   ├── audio/           # Audio engine
│   ├── midi/            # MIDI handling
│   ├── ui/              # Dioxus components
│   ├── effects/         # Built-in effects
│   ├── plugins/         # Plugin system
│   ├── scripting/       # Lua integration
│   └── collaboration/   # Nostr P2P
├── /assets/            # Static assets
├── /templates/         # Project templates
└── Cargo.toml           # Rust dependencies
```

---

## **Detailed Implementation Notes**

### **1. `.dioxmus` File Format**
- Use a structured format (e.g., JSON) for the `.dioxmus` file.
- Example structure:
```json
{
  "metadata": { "name": "My Project", "bpm": 120, "time_signature": "4/4" },
  "tracks": [
    {
      "type": "audio",
      "name": "Track 1",
      "audio_file": "path/to/audio.wav",
      "volume": 1.0,
      "effects": ["reverb", "delay"]
    },
    {
      "type": "midi",
      "name": "MIDI Track",
      "notes": [{"time": 0, "note": 60, "duration": 1, "velocity": 100}],
      "instrument": "synth"
    }
  ],
  "ui_state": { "theme": "dark", "layout": "default" },
  "plugins": [],
  "version": "1.0"
}
```
important the file is a archive that contains stuff like the audio files and the struktured data
### **2. Audio Engine**
- Use `cpal` for audio I/O.
- Implement a ring buffer for real-time audio processing.
- Use `fundsp` for DSP (filters, effects).

### **3. MIDI Support**
- Use `midir` for Rust MIDI support.
- Web MIDI API for browser compatibility.

### **4. Collaboration via Nostr**
- Use `nostr-rs` for Nostr client functionality.
- Implement a signaling server for initial peer discovery.
- Use WebRTC for real-time audio/data streaming.

### **5. Scripting with Lua**
- Use `mlua` for Lua scripting.
- Allow users to write custom effects/tools in Lua.

### **6. UI Components**
- Use Dioxus for UI components (buttons, sliders, piano roll).
- Custom SVG-based piano keyboard for note input.

### **7. Performance Optimizations**
- Use WASM for critical audio processing.
- Implement Web Workers for background tasks.

---

## **Expected Output**
The AI should:
1. Generate a **fully functional** Dioxus app with Rust backend.
2. Implement the `.dioxmus` file format and serialization/deserialization.
3. Build the audio engine, MIDI support, and plugin system.
4. Create a responsive, accessible UI with Dioxus.
5. Implement real-time collaboration via Nostr.
6. Provide a Lua scripting engine for extensibility.
7. Optimize performance for low-latency audio processing.
8. Include a `README.md` with setup, usage, and contribution guidelines.

---

## **Deliverables**
- Source code (Rust/Dioxus)
- `.dioxmus` file format specification
- Build instructions (Docker/Node.js setup)
- Example projects and templates
- Testing suite (unit/integration tests)
- Documentation (user manual, API docs)

---

## **Bonus Features (If Time Permits)**
- Cloud sync (optional, using Nostr relays).
- More advanced synth engines (FM, wavetable).
- AI-assisted mixing/mastering tools.
