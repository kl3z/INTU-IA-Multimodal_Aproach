# INTU-IA – Audio Transcription Evaluation (Whisper Integration)

This folder summarizes a key part of the development process for the **INTU-IA** system, specifically focusing on the **transcription of audio to text** using the [Whisper large model](https://openai.com/index/whisper/) developed by OpenAI([Radford et al., 2022](https://cdn.openai.com/papers/whisper.pdf)).

---

## Objective

Due to the unavailability of real interrogation recordings during the development phase, we adopted an **LLM-driven synthetic approach** to test and validate the transcription capabilities of the INTU-IA audio module.

---

## Methodology

### 1. Synthetic Interrogation Generation

Using **ChatGPT**, we generated 36 fictional police interrogation scripts by providing structured prompts with inputs such as:
- Topic of the interrogation
- Number of participants
- Behavioral attributes (e.g., posture, attitude)
- Scene setting

The generated interrogations are stored in:


---

### 2. Text-to-Video Synthesis with InVideo AI

To simulate real-world audio conditions, the scripts were converted into videos using [InVideo AI](https://invideo.io/), resulting in **36 synthetic videos**.

In addition, segments from the Portuguese legal drama *A Sentença* (TVI, 2024) were manually selected to evaluate transcription on naturally spoken Portuguese.

🔗 All videos are available here:  
[Google Drive – Video Corpus](https://drive.google.com/drive/folders/1xgyHinmyZtYfSghvwBGJwI-Jdt-jPaag?hl=pt-br)

---

### 3. Audio Transcription with Whisper

The following script performs audio-to-text transcription:


It prompts the user to upload a `.mp4` file and outputs the corresponding `.txt` transcription using Whisper (large model).

---

### 4. Noise Filtering & WER Evaluation

Since ChatGPT-generated scripts often include environmental and narrative noise, we created the script:


This script filters out non-dialogue content and produces:


Then, using the [JiWER](https://pypi.org/project/jiwer/) library, we computed the **Word Error Rate (WER)** by comparing Whisper's output to the cleaned reference.

---

## Results

| Source Type                      | Avg. WER |
|----------------------------------|----------|
| Videos generated via InVideo AI | 15.93%   |
| TV Series “A Sentença”          | 13.22%   |

The slightly higher WER in synthetic content likely results from TTS-like delivery and narrative distractions, while real dialogue—despite background noise—yields better performance.

---

## References

- OpenAI, “Whisper: Open-source speech recognition,” 2022. [Online]. Available: [https://openai.com/index/whisper/](https://openai.com/index/whisper/)
- Alec Radford et al., *Robust Speech Recognition via Large-Scale Weak Supervision*, 2022. [PDF](https://cdn.openai.com/papers/whisper.pdf)
- InVideo, [https://invideo.io/](https://invideo.io/)
- TVI, *A Sentença*, 2024. [IMDB](https://www.imdb.com/title/tt32119132/)

---

## Folder Contents

- `Interrogations_LLM's.docx` – Synthetic interrogation scripts
- `Transciption_Video_to_text.ipynb` – Whisper transcription notebook
- `WER.ipynb` – Preprocessing and WER computation
- `interrogatorio_respostas.csv` – Cleaned reference dataset


