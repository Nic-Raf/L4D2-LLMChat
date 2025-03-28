# L4D2-LLMChat

**Enhance your Left 4 Dead 2 experience by enabling survivor bots to chat intelligently using various Large Language Models (LLMs)!**

This project is an enhanced fork of **smilz0's original Dot4GPT** ([https://github.com/smilz0/Dot4GPT](https://github.com/smilz0/Dot4GPT)). It expands upon the original concept by adding support for multiple LLM providers and managing all survivor bots within a single application instance.

## Features

* **Multi-LLM Support:** Connect to various AI services:
  * OpenAI (GPT models)
  * Ollama (Run models like Llama3, Mistral, etc., locally)
  * Google (Gemini models)
  * Mistral AI API
  * Groq (Fast Llama3, Mixtral inference)
* **Single Instance, Multi-Bot:** Run just **one** instance of the application to handle chat for all 8 survivors.
* **Flexible Configuration:** Easily switch between LLM providers and configure API keys/models via a `settings.json` file.
* **In-Character Responses:** Uses system prompts to instruct the LLM to respond according to the survivor's personality.
* **Customizable System Prompts:** System prompts for each bot can now be stored in separate JSON files or default to the built-in prompts.
* **Conversation Context:** Maintains separate conversation histories for each bot.
* **Idle Timeout:** Automatically resets a bot's conversation context after a period of inactivity.
* **Real-time(ish) Interaction:** Monitors input files generated by the companion L4D2 addon and writes responses for the addon to read.

## Side Note

Since this is a multi-bot instance, certain adjustments in chat formatting can significantly improve response quality. Based on experiments, it's best to avoid commas and formalities when chatting with the bots. The system is optimized for quick, dynamic exchanges, and structuring your input correctly enhances bot responsiveness.

For optimal results:
- **Start your message with the bot's name,** followed directly by your chat. Best to avoid commas or any other symbols after the bots' name. Example:
  - `coach how are you doing?`
  - `nick is coach your best buddy?`
- **And if you ever want to switch bot response,** just type their name at the beginning then your message.
- **Keep interactions concise and direct** for a seamless experience.
- **You can spam chat**, but it's best to avoid multiple instances of chat at the same time, especially if you're running local LLMs. This prevents excessive resource usage, avoids running multiple requests at once, and helps **reduce hallucinations** in responses.

This approach ensures smooth bot-switching, maintains clarity in conversations, and optimizes system performance.

## Requirements

1. **Left 4 Dead 2**
2. **Left 4 GPT Addon** (Available on Steam Workshop, comes with Left 4 Lib Addon)[Install Here](https://steamcommunity.com/sharedfiles/filedetails/?id=3023020742)
3. **Left 4 Lib Addon** (If not available on your addon)
4. **.NET Runtime** (Version 6.0 or later) - [Download Here](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)
5. **API Keys / Local LLMs:**
   * OpenAI, Gemini, Mistral, Groq (API keys required)
   * Ollama (Local server & models required)

## Installation & Setup

1. **Download & Install Requirements**
2. **Get Application Files:** Download the latest release from [Releases](https://github.com/DrStr4Nge147/L4D2-LLMChat/releases/tag/V1.0)
3. **Extract/Place Files:** Put files in a dedicated folder (e.g., `C:\L4D2-LLMChat`)
4. **First Run:** Run `Dot4GPT.exe` to generate `settings.json`
5. **Configure `settings.json`** (See below)
   • Change the "Provider" of your choice: OpenAI, Gemini, Mistral, Groq, Ollama
   • And input your APIs and desired model of your choice, refer to your llm providers for the model name
7. **Run the Application**: Launch `Dot4GPT.exe`

## Configuration (`settings.json`)

```json
{
  "Provider": "Ollama",
  "IOPath": "C:\\Program Files (x86)\\Steam\\steamapps\\common\\Left 4 Dead 2\\left4dead2\\ems\\left4gpt",
  "ApiKey": "sk-...",
  "OpenAiModel": "gpt-3.5-turbo",
  "OllamaBaseUrl": "http://localhost:11434",
  "OllamaModel": "llama3",
  "GeminiApiKey": "AIzaSy...",
  "GeminiModel": "gemini-1.5-flash-latest",
  "MistralApiKey": "...",
  "MistralModel": "mistral-large-latest",
  "GroqApiKey": "gsk_...",
  "GroqModel": "llama3-8b-8192",
  "MaxTokens": 60,
  "MaxContext": 5,
  "ResetIdleSeconds": 120,
  "APIErrors": true,
}
```

Alternatively, you can provide separate JSON files for each bot's system prompt, modifying them by specifying in the configuration. Copy and paste the sample prompts.json. Place this prompts.json in the same directory of the Dot4GPT.exe. If not found it will use the default system prompt.

### Example `prompts.json`

```json
{
  "_fallback": "You are {BotName} from Left 4 Dead 2.",
  "bill": "You are Bill, a grizzled Vietnam veteran who's seen too much. You're cynical, pragmatic, and often gruff, but you have a hidden protective side for the group. Focus on survival tactics, no-nonsense observations, and maybe complain about your aching bones or the situation.",
  "francis": "You are Francis, a tough biker who hates almost everything (except maybe vests). Respond with heavy sarcasm, complaints about the situation or specific things (like stairs, woods, vampires), and a generally cynical, tough-guy attitude. Don't be afraid to boast, even if it's unfounded.",
  "louis": "You are Louis, an eternally optimistic IT systems analyst, maybe even a Junior Analyst. Focus on the positive, finding supplies (especially 'Pills here!'), keeping morale up, and sometimes making slightly nerdy or office-related comparisons. Stay helpful and upbeat even when things are bleak.",
  "zoey": "You are Zoey, a college student who was obsessed with horror movies before the outbreak. Use your knowledge of horror tropes to comment on the situation, sometimes sarcastically or with dark humor. You started naive but are resourceful and trying to stay tough, maybe showing occasional moments of weariness or sadness.",
  "coach": "You are Coach, a former high school health teacher and beloved football coach. Act as the team motivator, often using folksy wisdom, sports analogies, or talking about food (especially cheeseburgers or BBQ). Be encouraging ('Y'all ready for this?') but firm when needed. Focus on teamwork and getting through this.",
  "ellis": "You are Ellis, a friendly, talkative, and endlessly optimistic mechanic from Savannah. Tell rambling stories, especially about 'my buddy Keith', even if they aren't relevant. Be enthusiastic, sometimes naive, get excited easily, and occasionally mention something about cars, engines, or tools.",
  "nick": "You are Nick, a cynical gambler and likely con man, usually seen in an expensive (but now dirty) white suit. Be sarcastic, distrustful of others, complain frequently about the situation and the incompetence around you. Focus on self-interest initially, but maybe show rare glimpses of competence or reluctant cooperation.",
  "rochelle": "You are Rochelle, a low-level associate producer for a local news station. Try to maintain a professional and level-headed demeanor, even when things are falling apart. Make observations as if reporting on the scene, use clear communication, and sometimes show a bit of media-savvy cynicism or frustration with the chaos."
}
```


## Running the Application


1. Run `Dot4GPT.exe` (If running the first time, settings.json witll automatically be created).
2. Configure `settings.json` correctly.
3. Ensure local services (like Ollama) are running if selected.
4. If your using other free LLM providers, set up your own api key as well.
5. Run `Dot4GPT.exe` (Console window should appear).
6. Keep the application running while playing L4D2.
7. Chat messages in-game will now trigger bot responses.

Note: If at first it will not respond, just try chatting it again or you could check the cmd terminal if it's functioning properly.

## How It Works

1. Player types a message in L4D2.
2. The VScript addon writes the message to an input file.
3. The application detects the change, processes it, and sends it to the LLM.
4. The response is written to an output file.
5. The VScript addon reads the response and makes the bot say it.

## Acknowledgements

* Based on **Dot4GPT** by smilz0 ([GitHub](https://github.com/smilz0/Dot4GPT))
* Thanks to developers of the various LLM APIs and .NET libraries used.
