<template>
    <div class="p-4 h-screen">
      <p class="text-lg">Terminal Blog - Type a command:</p>
      <pre class="mt-4">{{ output }}</pre>
      <input
        type="text"
        v-model="command"
        @keyup.enter="executeCommand"
        class="w-full bg-transparent text-terminalText border-none focus:outline-none mt-2"
        autofocus
      />
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        command: "",
        output: "Welcome to Terminal Blog! Type 'help' for commands.",
        typingIndex: 0,
        typingSpeed: 50, // Harf başına yazma hızı (ms)
      };
    },
    methods: {
      executeCommand() {
        const cmd = this.command.toLowerCase();
        this.command = ""; // Komut satırını temizle
  
        if (cmd === "help") {
          this.slowType([
            "Available commands:",
            "- info: About me",
            "- clear: Clear the screen",
            "- help: Show available commands",
          ]);
        } else if (cmd === "info") {
          this.slowType([
            "Hello! My name is Mert Ayhan.",
            "I am a software engineer interested in AI, full-stack development, and DevOps.",
            "I love coding and astronomy!",
          ]);
        } else if (cmd === "clear") {
          this.output = "";
        } else {
          this.slowType([`Command not found: ${cmd}`]);
        }
      },
      slowType(lines) {
        this.output = ""; // Önce terminali temizleyelim
        let currentLine = 0;
  
        const typeNextLine = () => {
          if (currentLine < lines.length) {
            let line = lines[currentLine];
            let typedText = "";
            let i = 0;
  
            const typeCharacter = () => {
              if (i < line.length) {
                typedText += line[i];
                this.output = this.output + "\n" + typedText;
                i++;
                setTimeout(typeCharacter, this.typingSpeed);
              } else {
                currentLine++;
                setTimeout(typeNextLine, 500); // Satır bitince biraz bekle
              }
            };
  
            typeCharacter();
          }
        };
  
        typeNextLine();
      },
    },
  };
  </script>
  
  <style scoped>
  /* Terminal Görünümü */
  body {
    background-color: black;
    color: #00ff00;
    font-family: "Courier New", monospace;
  }
  input {
    border: none;
    outline: none;
    color: #00ff00;
    background: transparent;
  }
  </style>
  