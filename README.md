# Deep Fried Headsets - SPT 4.0 Version

A server mod that enhances headset audio properties in SPT (Single Player Tarkov).

## Original Author
- shwng

## Requirements
- SPT 4.0.11 or compatible version
- .NET 9.0 SDK (for building from source)

## Installation (Pre-built)
1. Copy the `DeepFriedHeadsets.dll` file to your `SPT/user/mods/` folder
2. Copy the `config` folder next to the DLL
3. Start the SPT server

## Building from Source
1. Install the [.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)
2. Open a terminal in the mod folder
3. Run `dotnet build -c Release`
4. The compiled mod will be in `bin/Release/DeepFriedHeadsets/DeepFriedHeadsets/`

## Configuration
Edit `config/config.json` to adjust headset audio settings.

All values are **multipliers** unless noted with `Add` (additive) or `Set` (direct set).

### Volume Controls
- **AmbientVolume**: Multiplier for ambient noise reduction. Server's AmbientVolume is multiplied by this value. Most headsets have negative values (e.g., -50), so increasing this multiplier increases ambient noise reduction. However, If you want to reduce ambient sound, increase AmbientCompressorSendLevel instead.
- **HeadphonesMixerVolume**: Overall headset volume multiplier. Higher values = louder output.
- **DryVolume**: Multiplier for unprocessed (dry) audio signal. This determines how much "outside" sound is mixed to the headset's processed sound.
- **EffectsReturnsGroupVolumeSet**: This is the volume of sound effects (echo, reverb etc). Some ambient and wilderness effects in game use these effects.

### Compressor Settings
- **CompressorGain**: Multiplier for compressor output gain. Higher values boost quiet sounds.
- **CompressorThreshold**: Multiplier for compression threshold. Affects when compression kicks in.
- **CompressorAttack**: Multiplier for compressor attack time. How quickly compression engages.
- **CompressorRelease**: Multiplier for compressor release time. How quickly compression disengages.

> **How it works**: Imagine headsets have an automatic volume knob. When you fire a loud gun, the headset quickly turns the volume down (Attack time). When you stop shooting, it slowly turns the volume back up (Release time). The Threshold decides how loud a sound needs to be before this kicks in, and Gain boosts everything after. 

### Compressor Send Levels
- **AmbientCompressorSendLevel**: Multiplier for how much ambient audio is sent to the compressor. This is the actual ambient noise reduction. Most headsets have a negative value for this. So by multiplying this by 2 you increase ambient noise reduction by 2. 
- **ClientPlayerCompressorSendLevelSet**: This is how much your own sounds (like running etc) is sent to the headset's compressor.
- **PlayerCompressorSendLevel**: This is how much bot sounds (like running etc) is sent to the headset's compressor.
- **GunsCompressorSendLevelAdd**: This is how much gun sounds (like shooting, reloading, switching tactical devices etc) is sent to the headset's compressor.
- **EffectsReturnsCompressorSendLevelSet**: This is how much sound effects (echo, reverb etc) are returned to the headset compressor. Some ambient and wilderness effects in game use these effects.

### EQ Settings
- **EQBandGain**: Multiplier applied to all EQ band gains (bands 1-3).
- **EQBandFrequency**: Multiplier applied to all EQ band frequencies.
- **EQBandQ**: Multiplier applied to all EQ band Q values (bandwidth).
> **Note**: Just leave them as is. 

### Filter Settings
- **HighpassFreq**: Multiplier for highpass filter cutoff frequency.
- **HighpassResonance**: Multiplier for highpass filter resonance.
- **LowpassFreq**: Multiplier for lowpass filter cutoff frequency.
> **Note**: Just leave them as is. 

### Distortion
- **DistortionMultiplier**: Multiplier for audio distortion amount. Lower values reduce distortion.

### Spatial
- **RolloffMultiplier**: Controls distance-based volume falloff. Values near 1.0 maintain original behavior. Don't increase this too much as it makes distant sounds sound like its closer to you.

### UPDATING FROM PREVIOUS CONFIG
- If you've set a custom config previously, please rename "AmbientCompressorSendLevelAdd" to "AmbientCompressorSendLevel" in config.json. And give it a value between 1-2. Other values are the same.

## Changes from 3.x Version
- Rewritten from TypeScript to C# for SPT 4.0 compatibility
- Uses the new SPTarkov.Server.Core NuGet packages
- Config format changed from JSONC to JSON (comments not supported in JSON)

## License
MIT
