# 🎧 DJ Remix Studio Pro

A browser-based music creation tool with 46 synthesized instruments and a grid sequencer for creating electronic music, beats, and melodies.

![Version](https://img.shields.io/badge/version-1.0-blue)
![HTML5](https://img.shields.io/badge/HTML5-orange)
![JavaScript](https://img.shields.io/badge/JavaScript-yellow)
![Web Audio API](https://img.shields.io/badge/Web%20Audio%20API-green)

## 🚀 Quick Start

1. Download `music.html`
2. Open the file in any modern web browser (Chrome, Firefox, Safari, Edge)
3. Start creating music!

Try DEMO [here](https://rikiza.pythonanywhere.com/music)

**No installation, no server, no dependencies required!**

## ✨ Features

### 🎹 46 Instruments
- **🥁 Drums (7)**: Kick, Snare, Hi-Hat, Clap, Tom, Cymbal, Rimshot
- **🎹 Bass (7)**: Bass Synth, Sub Bass, Wobble, Reese, Acid Bass, FM Bass, Distorted Bass
- **🎵 Leads (8)**: Lead Synth, Pluck, Square Lead, Saw Lead, Supersaw, Arpeggio, Pulse Lead, Sync Lead
- **🎶 Pads & Chords (6)**: Pad, Strings, Choir, Brass, Ambient Pad, Warm Pad
- **🔊 FX & Special (11)**: Siren, Riser, Sweep, Vocal Stab, White Noise, Vinyl Crackle, Laser Zap, Explosion, Glitch, Alarm, Robot Voice
- **🎸 Organic (5)**: Bell, Marimba, Piano, Guitar, Organ

### 🎚️ Professional Controls
- **Sidebar Panel** with organized sections
- **BPM Control** (60-200 BPM)
- **Tap Tempo** - tap button to set tempo
- **Master Volume** control
- **Metronome** for timing guidance
- **Master Loop** toggle

### 🎵 Track Features
- **Grid-based sequencer** (like FL Studio/Ableton)
- **Multiple tracks** with different instruments
- **Configurable track length** (8, 16, 32, 64 steps)
- **Configurable rows** (4, 8, 12, 16 pitches)
- **Per-track controls**:
  - 🔊 Volume slider
  - 🔇 Mute button
  - S Solo button
  - 🔁 Repeat toggle
  - ✕ Delete track

### 💾 Project Management
- **Save projects** to browser localStorage
- **Load projects** from saved data
- **Project naming**

### 📱 Mobile Responsive
- Works on desktop, tablet, and mobile devices
- Collapsible sidebar with menu button
- Touch-optimized interface

## 📖 How to Use

### Creating Your First Track

1. **Select an Instrument**
   - Choose from the dropdown in the sidebar (e.g., "Kick Drum")

2. **Set Track Properties**
   - Grid Rows: Number of pitches (default: 8)
   - Track Length: Number of steps (default: 16)

3. **Add Track**
   - Click "➕ Add Track" button

4. **Add Notes**
   - Click on grid cells to activate notes (they turn purple)
   - Click again to deactivate
   - Each column = one beat/step
   - Each row = different pitch (lower = bass, higher = treble)

5. **Adjust Settings**
   - Use volume slider per track
   - Toggle repeat (🔁) to loop the track
   - Use mute (🔇) to silence specific tracks
   - Use solo (S) to hear only that track

6. **Play Your Music**
   - Click "▶ Play" to start playback
   - Click "⏹ Stop" to stop

### Advanced Features

#### Building a Beat
```
1. Add Kick Drum track (16 steps, 8 rows)
   - Place kicks on steps 1, 5, 9, 13 (every 4 beats)

2. Add Snare track
   - Place snares on steps 5, 13 (backbeat)

3. Add Hi-Hat track
   - Place hi-hats on every step (or every 2 steps)

4. Press Play!
```

#### Creating Melodies
```
1. Add Lead Synth or Pluck track
2. Use different rows for different notes
3. Create patterns across 16 or 32 steps
4. Adjust BPM for desired speed
```

#### Using Repeat & Loop
- **Track Repeat (🔁)**: Individual track loops continuously
- **Master Loop**: Global control for all repeating tracks
- Example: 8-step drum loop + 32-step melody

### Tips & Tricks

🎯 **Grid Layout**
- Vertical bars every 4 beats = measure markers
- Higher rows = higher pitch
- Lower rows = lower pitch/bass

🎹 **Instrument Tips**
- **Drums**: Don't need pitch variation, use any row
- **Bass**: Use lower rows for deeper sound
- **Leads/Melodies**: Use multiple rows for different notes
- **Pads**: Layer with other instruments for depth

⏱️ **Tempo Tips**
- **60-90 BPM**: Hip-hop, chill, ambient
- **90-120 BPM**: Pop, rock, general music
- **120-140 BPM**: House, techno, electronic
- **140-200 BPM**: Drum & bass, hardcore

🎚️ **Mixing Tips**
1. Start with drums at 70% volume
2. Add bass at 60-70%
3. Add melodies at 50-60%
4. Use mute/solo to hear individual tracks
5. Adjust master volume to avoid distortion

## 🔧 Technical Details

### Browser Requirements
- Modern browser with Web Audio API support
- Chrome 34+, Firefox 25+, Safari 14+, Edge 79+
- JavaScript enabled

### Audio Engine
- **Web Audio API** for sound synthesis
- **Real-time synthesis** - no audio files needed
- **ADSR envelopes** for realistic instrument sounds
- **Filters and effects** for each instrument
- **Master gain node** for volume control

### Storage
- Uses browser **localStorage** for saving projects
- Data persists between sessions
- No server/cloud storage required

## 🎨 Customization

Want to modify the app? Here's where to look:

### Add New Instruments
Edit the `instruments` object:
```javascript
instruments.myNewSound = {
    play: (time, volume, freq) => {
        const osc = audioContext.createOscillator();
        const gain = audioContext.createGain();
        osc.type = 'sine';
        osc.frequency.value = freq;
        gain.gain.setValueAtTime(volume * 0.5, time);
        gain.gain.exponentialRampToValueAtTime(0.01, time + 0.5);
        osc.connect(gain);
        gain.connect(masterGainNode);
        osc.start(time);
        osc.stop(time + 0.5);
    }
};
```

### Change Colors
Edit CSS in `<style>` section:
```css
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
```

### Modify Default Settings
Change values in Track class constructor:
```javascript
this.rows = 8;      // Default rows
this.length = 16;   // Default steps
this.volume = 0.7;  // Default volume
```

## 🐛 Troubleshooting

**No sound when playing?**
- Make sure device volume is up
- Check if notes are placed on grid (purple cells)
- Ensure track is not muted (🔇 should not be highlighted)
- Click on page first (browsers require user interaction for audio)

**Playback is laggy?**
- Reduce number of active tracks
- Lower BPM
- Use shorter track lengths
- Close other browser tabs

**Mobile issues?**
- Use landscape orientation
- Tap ☰ Menu to access sidebar
- Ensure touch is enabled in browser

**Project won't save?**
- Check if localStorage is enabled
- Private/Incognito mode may block localStorage
- Clear browser cache if storage is full

## 📱 Mobile Usage

### Accessing Sidebar
1. Tap the **☰ Menu** button (top-left)
2. Sidebar slides in from left
3. Tap outside sidebar to close

### Adding Notes
- Tap grid cells to activate/deactivate
- Scroll horizontally to see all steps
- Pinch to zoom if needed

## 🎵 Example Projects

### Four-on-the-floor (House beat)
```
BPM: 128
- Kick Drum: Steps 1, 5, 9, 13
- Hi-Hat: Every 2nd step
- Snare: Steps 5, 13
```

### Hip-hop beat
```
BPM: 90
- Kick: Steps 1, 7, 11
- Snare: Steps 5, 13
- Hi-Hat: Every step
```

### Melodic Pattern
```
BPM: 120
- Pluck: Create pattern using rows 3-8
- Pad: Hold notes on rows 5-7
- Bass: Low notes on rows 0-2
```

## 🌟 Project Structure

```
main root       # Repository folder
├── music.html         # music file
├── README.md          # this file
└── LICENSE.md         # MIT LICENSE file
```

## 🤝 Contributing

Contributions welcome!

### How to Contribute
1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

### Ideas for Contribution
- Add new instruments
- Implement effects (reverb, delay, filter)
- Add keyboard shortcuts
- Create preset patterns
- Improve mobile UI
- Add export to WAV/MP3
- Implement MIDI support

## 📄 License

MIT License - Free to use and modify for personal and commercial projects.

## 🎓 Learning Resources

### Web Audio API
- [MDN Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API)
- [Web Audio API Book](https://webaudioapi.com/)

### Music Theory Basics
- Note frequencies and scales
- BPM and tempo
- Rhythm patterns
- Sound synthesis

## ❓ FAQ

**Q: Can I export my music to MP3?**  
A: Currently no, but you can record system audio using external software.

**Q: Does it work offline?**  
A: Yes! Once loaded, it works completely offline.

**Q: Can I share my projects?**  
A: Projects are saved locally. You can manually export/import using browser tools.

**Q: Why is there no sound?**  
A: Most likely no notes are placed. Click grid cells to add notes (they turn purple).

**Q: Can I use this commercially?**  
A: Yes, it's free for any use.

## 🔗 Links

- [Report Bug](https://github.com/Rikiza89/Let-s-music/issues)
- [Request Feature](https://github.com/Rikiza89/Let-s-music/issues)
- [Discussions](https://github.com/Rikiza89/Let-s-music/discussions)

## 🙏 Acknowledgments

- Web Audio API community
- Electronic music producers for inspiration
- Open source contributors

---

**Made with ❤️ for music creators**

🎧 Happy music making! 🎵

*Star ⭐ this repo if you found it useful!*
