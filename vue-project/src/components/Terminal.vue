<template>
  <div class="bg-black h-screen p-6 font-mono text-green-400 overflow-hidden">
    <!-- Terminal Başlık -->
    <div class="flex items-center mb-4">
      <div class="w-3 h-3 bg-red-500 rounded-full mr-2"></div>
      <div class="w-3 h-3 bg-yellow-500 rounded-full mr-2"></div>
      <div class="w-3 h-3 bg-green-500 rounded-full"></div>
      <p class="ml-4 text-sm">Terminal Blog - Mert Ayhan</p>
    </div>

    <!-- Terminal Ekranı -->
    <div class="bg-gray-900 p-4 rounded-lg h-[80vh] overflow-y-auto shadow-2xl border border-gray-800">
      <!-- Çıktılar -->
      <pre class="whitespace-pre-wrap break-words text-sm leading-6">{{ output.join("\n") }}</pre>

      <!-- Komut Girişi -->
      <div class="flex items-center mt-2">
        <span class="text-green-400 mr-2">$</span>
        <input
          type="text"
          v-model="command"
          @keyup.enter="executeCommand"
          class="w-full bg-transparent text-green-400 border-none focus:outline-none"
          autofocus
          placeholder="Type a command..."
        />
      </div>
    </div>

    <!-- Footer (Ekstra Bilgi) -->
    <div class="mt-4 text-center text-gray-500 text-sm">
      <p>Press <span class="text-green-400">Enter</span> to execute commands. Type <span class="text-green-400">help</span> for a list of commands.</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      command: "",
      output: ["Welcome to Terminal Blog! Type 'help' for commands."],
      typingSpeed: 30, // Yazı hızı artırıldı
    };
  },
  methods: {
    executeCommand() {
      const cmd = this.command.toLowerCase();
      this.command = "";

      if (cmd === "help") {
        this.slowType([
          "Available commands:",
          "- info: About me",
          "- projects: My projects",
          "- skills: My technical skills",
          "- experience: My professional experience",
          "- contact: My contact information",
          "- clear: Clear the screen",
          "- help: Show available commands",
        ]);
      } else if (cmd === "info") {
        this.slowType([
          "Hello! My name is Mert Ayhan.",
          "I am a 4th-year student at Balıkesir University, Department of Electrical and Computer Engineering.",
          "My passion lies in software development, particularly in web development, AI, machine learning, and game development.",
          "I am deeply interested in astronomy and physics, which inspire my creative solutions in technology.",
        ]);
      } else if (cmd === "projects") {
        this.slowType([
          "Here are some of my notable projects:",
          "- Sentiment Analysis: A project analyzing YouTube comments using TensorFlow, categorizing them into positive, negative, and neutral.",
          "- Currency Prediction: A machine learning project predicting currency exchange rates.",
          "- Movie Genre Classification: A project classifying movie genres using ML algorithms.",
          "- Full-Stack Web Applications: Developed various web apps using React, Next.js, Node.js, and Express.",
          "- Mobile Apps: Built cross-platform mobile applications using Flutter.",
        ]);
      } else if (cmd === "skills") {
        this.slowType([
          "Technical Skills:",
          "- Frontend: React, Next.js, Flutter, HTML, CSS, JavaScript",
          "- Backend: Node.js, Express.js, REST APIs",
          "- AI/ML: TensorFlow, Python, Scikit-learn",
          "- Databases: MongoDB, Firebase",
          "- Tools: Git, Docker, Linux",
          "- Languages: JavaScript, Python, Dart, C/C++",
        ]);
      } else if (cmd === "experience") {
        this.slowType([
          "Professional Experience:",
          "- Full-Stack Developer: Over 2 years of experience building web and mobile applications.",
          "- Internship in Defense Industry: Gained practical experience in software development processes.",
          "- President of Balıkesir University Electrical and Computer Systems Community: Developed leadership and project management skills.",
        ]);
      } else if (cmd === "contact") {
        this.slowType([
          "Contact Information:",
          "- Email: mertayhandev@gmail.com",
          "- LinkedIn: https://www.linkedin.com/in/mert-ayhan-0bb469233/",
          "- GitHub: https://github.com/mertayhan123",
        ]);
      } else if (cmd === "clear") {
        this.output = [];
      } else {
        this.slowType([`Command not found: ${cmd}`]);
      }
    },
    slowType(lines) {
      let currentLine = 0;

      const typeNextLine = () => {
        if (currentLine < lines.length) {
          let line = lines[currentLine];
          let typedText = "";
          let i = 0;

          const typeCharacter = () => {
            if (i < line.length) {
              typedText += line[i];
              this.output[this.output.length - 1] = typedText;
              i++;
              setTimeout(typeCharacter, this.typingSpeed);
            } else {
              currentLine++;
              if (currentLine < lines.length) {
                this.output.push("");
                setTimeout(typeNextLine, 500);
              }
            }
          };

          this.output.push("");
          typeCharacter();
        }
      };

      typeNextLine();
    },
  },
};
</script>

<style scoped>
/* Özel stiller */
input::placeholder {
  color: #4a5568; /* Gri renk */
}
</style>