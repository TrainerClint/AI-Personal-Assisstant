Core problems:- 
1. Dependancy on internet for AI access
2. Privacy concerns.

Inputs and outputs:- 
Input> 
1. Microphone → Voice commands 
2. Keyboard → Text prompts
3. Config Files → Model paths, app locations
4. Settings →Timeout values, audio buffer sizes

Output:>
1. Screen → Status messages, AI responses, time
2. Browser → Opens websites (Google, YouTube)
3. Apps → Launches VSCode, Discord, Spotify, Calculator
4. Windows → Locks screen, shows time, shutdown/restart
5. Console → Debug logs, intent detection, errors

Workflow Logic
1. Passive Listening → Vosk continuously processes audio chunks
2. Wake Word Detection → "john" in partial/final → Activate(wake word currently set to "john")
3. Active Listening → 8s window for command → Vosk STT → text
4. Intent Classification → Regex matching → {open_app, open_web, system_cmd, llama_query}
5. Action Execution → Route to handler → subprocess/webbrowser/API call
6. Response → Console output → Return to passive listening

Tools/APIs used:
1. Vosk → Wake word + command recognition
2. Ollama → Core for locally processing queries 
3. PyAudio → Microphone input
4. subprocesses,ctypes → App launch, lock/shutdown
5. webbrowser → Website opening
6. re(regex) → Intent matching

Failure cases and limitations:
1. Wake Word Miss → Background noise, accent, mic quality
2. Command Misrecognition → Vosk small model accuracy (~85-90%)
3. Regex Miss → Unseen phrasing ("please open chrome")
4. LLM Timeout → Long responses on 70B models
5. App Path Errors → Apps moved/reinstalled
6. Single-User → No multi-speaker isolation
7. Desktop Only → Windows-specific paths
8. No TTS (text-to-speech) output → responses are console-only

Redesigning if building it again:
1. Replace Regex with ML Intent Classifier
2. Add TTS Output
3. Productionize: Docker containerization,Logging (structured JSON),etc
4. Barge-in capability (interrupt ongoing speech)




