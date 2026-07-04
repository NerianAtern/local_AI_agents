# local_AI_agents
Function-based AI agent running with a local-machine model.


### Idea
Stufe 1: Der "Ein-Skript-Agent" (Sehr einfach)
Das ist der perfekte Start. Du schreibst ein einziges Skript (z. B. in Python). Du nutzt ein Feature namens Function Calling (Funktionsaufruf).

Wie es funktioniert: Du gibst dem LLM eine Liste von normalen Programmierfunktionen, die du geschrieben hast (z. B. schreibe_datei(dateiname, inhalt) oder hole_wetter(stadt)). Du fragst die KI: "Der Nutzer will wissen, wie das Wetter in Hamburg ist. Was soll ich tun?" Die KI führt die Funktion nicht selbst aus, aber sie antwortet dir im JSON-Format: {"funktion": "hole_wetter", "ort": "Hamburg"}. Dein Code liest dieses JSON, führt deine Funktion aus und schickt das Ergebnis zurück an die KI.

Schwierigkeit: 2/10. Wenn du weißt, wie man eine API aufruft und ein JSON liest, kriegst du das an einem Nachmittag hin.

Für Entwickler gibt es heute ein Tool, das der absolute Goldstandard für lokale KI ist: Ollama.Ollama läuft unauffällig im Hintergrund, verbraucht nur dann nennenswert Hardware-Ressourcen, wenn du es aktiv ansprichst, und stellt dir sofort eine lokale API bereit. Das ist genau die Schnittstelle, die du später brauchst, um die KI mit deinem eigenen Code (z. B. in Python oder Go) anzusteuern.Ein kurzer Hardware-Check vorab: Für die gängigen, intelligenten Allrounder-Modelle sollte dein PC mindestens 16 GB RAM (oder einen Mac mit M-Chip) besitzen. Wenn du weniger hast, ist das auch kein Weltuntergang – dann weichst du einfach auf extrem leichtgewichtige Modelle aus.Hier ist der schnellste Weg, um deine eigene KI offline zu starten:1.Ollama installieren:1-2 Minuten.Gehe auf die offizielle Website ollama.com und lade den Installer für Windows oder macOS herunter. Wenn du auf Linux unterwegs bist, reicht dieser einfache Befehl im Terminal:Bashcurl -fsSL https://ollama.com/install.sh | sh
2.Das Sprachmodell herunterladen und starten:Abhängig von deiner Internetleitung.Öffne dein Terminal (unter Windows die Eingabeaufforderung) und starte dein erstes Modell. Wir nutzen hier das extrem starke und effiziente Qwen3 (8B):Bashollama run qwen3:8b
Ollama lädt das Modell nun automatisch herunter (ca. 4,8 GB). Sobald der Download abgeschlossen ist, verändert sich die Eingabezeile und du kannst direkt im Terminal live und komplett offline mit deiner KI chatten.3.Den Chat beenden:Sofort.Wenn du genug gefragt hast, tippe einfach /bye in das Chat-Terminal. Die Session wird geschlossen und Ollama gibt den Arbeitsspeicher deines PCs wieder komplett frei.Der Clou für Software-EinsteigerDa du programmieren kannst, kommt jetzt der eigentlich spannende Teil. Während Ollama läuft, horcht es im Hintergrund auf dem Port 11434. Du kannst die KI also über ein ganz normales HTTP-Request (zum Beispiel mit curl im Terminal) ansprechen:Bashcurl http://localhost:11434/api/generate -d '{
  "model": "qwen3:8b",
  "prompt": "Schreibe eine ultrakurze Begrüßung für einen Programmierer.",
  "stream": false
}'
Du brauchst also keine teuren Cloud-Keys von OpenAI oder Anthropic und musst keine Kreditkarte hinterlegen. Du installierst dir in Python einfach die Bibliothek mit pip install ollama, tippst ein paar Zeilen Code und schon hast du die perfekte Basis, um deinen ersten eigenen autonomen Agenten zu bauen.Tipp für UI-Liebhaber: Falls dir das Terminal auf Dauer zu trocken ist und du eine Oberfläche wie bei ChatGPT bevorzugst, installiere dir LM Studio. Das ist eine schicke Desktop-App, bei der du Open-Source-Modelle per Mausklick suchen, herunterladen und in einem modernen Chat-Fenster nutzen kannst.
