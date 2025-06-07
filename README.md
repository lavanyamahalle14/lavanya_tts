# Multilingual Text-to-Speech (TTS) System Setup Guide

This guide will help you set up the Multilingual TTS system with FastSpeech2 and HiFi-GAN support.

## System Requirements

- Operating System: Windows/Linux/MacOS
- Python version: 3.10 (recommended)
- GPU: CUDA-compatible GPU (optional, for faster processing)
- Storage: At least 10GB free space (for models and dependencies)

## Step-by-Step Setup Guide

### 1. Set up Python Environment

First, install Conda if you haven't already. Download from: https://docs.conda.io/en/latest/miniconda.html

```bash
# Create a new conda environment
conda create -n tts_env python=3.10
conda activate tts_env
```

### 2. Install Core Dependencies

```bash
# Install PyTorch and TorchAudio
conda install pytorch torchaudio -c pytorch

# Install basic requirements
pip install flask==3.1.0
pip install numpy>=2.2.5
pip install scipy>=1.15.3
pip install PyYAML>=6.0.2
```

### 3. Install TTS-Specific Dependencies

```bash
# Install ESPnet and related packages
pip install espnet
pip install espnet2
pip install soundfile

# Install language processing tools
pip install indic-num2words
pip install nltk
pip install indic-unified-parser
pip install pandas

# Install utilities
pip install matplotlib
pip install requests
pip install gunicorn  # For production deployment
```

### 4. Download and Setup Project

```bash
# Clone the repository (if using git)
git clone [your-repository-url]
cd [project-directory]

# Or download and extract the project files to your desired location
```

### 5. Directory Structure Setup

Ensure you have the following directory structure:
```
.
├── app.py                  # Flask application
├── Fastspeech2_HS/        # Core TTS engine
│   ├── inference.py       # TTS inference script
│   ├── phone_dict/       # Phone dictionaries for all languages
│   └── [language]/       # Language-specific models
├── static/
│   └── audio/            # Generated audio files
└── templates/
    └── index.html        # Web interface
```

### 6. Model Setup

1. Create necessary directories:
```bash
mkdir -p static/audio
```

2. Ensure model files are in place:
- Phone dictionaries should be in `Fastspeech2_HS/phone_dict/[language]`
- Model files should be in `Fastspeech2_HS/[language]/[gender]/model/model.pth`

### 7. Running the Application

```bash
# Activate the environment (if not already activated)
conda activate tts_env

# Start the Flask application
python app.py
```

The application will be available at: `http://localhost:4005`

### 8. Verify Installation

1. Open your web browser and navigate to `http://localhost:4005`
2. Select a language from the dropdown
3. Choose gender and speed options
4. Enter some text
5. Click "Generate Speech" to test

## Supported Languages

- Hindi
- Marathi
- Punjabi
- Tamil
- Telugu
- Kannada
- Malayalam
- Gujarati
- Bengali
- Odia
- Assamese
- Manipuri
- Bodo
- Rajasthani
- Urdu
- English

## Troubleshooting

1. If you see Flash Attention warning:
   ```
   Failed to import Flash Attention, using ESPnet default: No module named 'flash_attn'
   ```
   This is normal and can be safely ignored.

2. If you encounter CUDA errors:
   - Ensure you have CUDA installed if using GPU
   - Try running on CPU by setting appropriate environment variables

3. If models are not loading:
   - Check if model files are in correct directories
   - Verify file permissions
   - Check console for specific error messages

4. For package conflicts:
   ```bash
   # Create a fresh environment
   conda deactivate
   conda env remove -n tts_env
   conda create -n tts_env python=3.10
   conda activate tts_env
   ```
   Then follow the installation steps again.

## Quick Commands Reference

```bash
# Start application
conda activate tts_env && python app.py

# Kill existing process and restart (if needed)
pkill -f "python app.py" && conda activate tts_env && python app.py

# Check installed packages
pip list
```

## Additional Notes

- Keep your conda environment activated while working with the project
- Regular updates to dependencies might be required for security patches
- Backup your model files before any major updates
- For production deployment, consider using gunicorn with Flask

## Support

For issues and questions:
1. Check the troubleshooting section
2. Verify your Python and package versions
3. Ensure all model files are in place
4. Check system requirements are met 






from pd
pkill -f "python app.py" && conda activate tts_env && python app.py
conda create -n tts_env python=3.10 -y
conda activate tts_env && pip install torch torchaudio espnet pandas num2words indic-unified-parser flask nltk
python app.py

cd Fastspeech2_HS && python inference.py --sample_text "नमस्कार" --language marathi --gender male --alpha 1.0 --output_file output_marathi.wav