<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=200&section=header&text=The%20Raider&fontSize=80&fontAlignY=35&animation=fadeIn&fontColor=fff" width="100%"/>
  
  <!-- Typing SVG -->
  <a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&center=true&width=435&lines=Professional+FiveM+Developer;Premium+Script+Creator;UI%2FUX+Designer;Security+Expert" alt="Typing SVG" /></a>
  
  <!-- Badges -->
  <p>
    <a href="https://www.youtube.com/channel/UCw11VeGY4MFKItj0FGm7FUQ"><img src="https://img.shields.io/badge/YouTube-FF0000?style=flat-square&logo=youtube&logoColor=white" alt="YouTube"/></a>
    <a href="https://discord.gg/EkwWvFS"><img src="https://img.shields.io/badge/Discord-7289DA?style=flat-square&logo=discord&logoColor=white" alt="Discord"/></a>
    <a href="https://eyestore.tebex.io/"><img src="https://img.shields.io/badge/Tebex-5CAD3A?style=flat-square&logo=shopify&logoColor=white" alt="Tebex"/></a>
    <img src="https://komarev.com/ghpvc/?username=raiderss&style=flat-square&color=6cd63e" alt="Profile Views"/>
  </p>
</div>

<h2 align="center">🔥 Premium FiveM Developer 🔥</h2>

<!-- Tech Animation -->
<p align="center">
  <img src="https://raw.githubusercontent.com/rodrigograca31/rodrigograca31/master/matrix.svg" width="800" height="100">
</p>

<!-- About Section -->
```javascript
const raider = {
  name: "The Raider",
  title: "FiveM Developer & UI Designer",
  location: "Worldwide Remote",
  specialization: [
    "FiveM Script Development",
    "QBCore Framework Expert", 
    "ESX Framework Expert",
    "Server Security Solutions",
    "UI/UX Design",
    "Shop & Menu Systems"
  ],
  skills: {
    languages: ["Lua", "JavaScript", "HTML", "CSS", "SQL"],
    frameworks: ["QBCore", "ESX", "vRP", "jQuery", "VueJS"],
    tools: ["Git", "VSCode", "Figma", "Photoshop", "MySQL/SQLite"]
  },
  contact: {
    discord: "https://discord.gg/EkwWvFS",
    store: "https://eyestore.tebex.io/",
    youtube: "https://www.youtube.com/channel/UCw11VeGY4MFKItj0FGm7FUQ"
  }
};
```

<!-- Mini Game Section -->
<h2 align="center">🎮 Raider Runner - Mini Game</h2>
<p align="center">Try my mini ASCII game! Press Space to start and jump.</p>

<pre align="center" id="game">
+-------------------------------------------------------------------+
|                                                                   |
|                                                                   |
|                                 🦖                                |
|                 🌵                               🌵              |
+-------------------------------------------------------------------+
</pre>

<details>
  <summary align="center"><b>👆 Click to view game instructions and code</b></summary>

```javascript
// Raider Runner Game - Offline Dinosaur Runner Clone
// Created by The Raider for FiveM servers
// Visit my GitHub: https://github.com/raiderss

class Game {
  constructor() {
    this.canvas = document.createElement('canvas');
    this.ctx = this.canvas.getContext('2d');
    this.width = 800;
    this.height = 200;
    this.dino = { x: 50, y: 150, width: 40, height: 60, jumping: false, yVelocity: 0 };
    this.obstacles = [];
    this.score = 0;
    this.speed = 5;
    this.gameOver = false;
    this.lastObstacleTime = 0;
    
    document.body.appendChild(this.canvas);
    document.addEventListener('keydown', this.handleKeyDown.bind(this));
    
    this.mainLoop();
  }
  
  handleKeyDown(e) {
    if (e.code === 'Space' && !this.dino.jumping && !this.gameOver) {
      this.dino.jumping = true;
      this.dino.yVelocity = -12;
    } else if (e.code === 'Space' && this.gameOver) {
      this.reset();
    }
  }
  
  update() {
    // Update dino
    if (this.dino.jumping) {
      this.dino.y += this.dino.yVelocity;
      this.dino.yVelocity += 0.8;
      
      if (this.dino.y >= 150) {
        this.dino.y = 150;
        this.dino.jumping = false;
      }
    }
    
    // Generate obstacles
    const now = Date.now();
    if (now - this.lastObstacleTime > 1500 + Math.random() * 1000) {
      this.obstacles.push({
        x: this.width,
        y: 150,
        width: 20 + Math.random() * 30,
        height: 40 + Math.random() * 20
      });
      this.lastObstacleTime = now;
    }
    
    // Update obstacles
    for (let i = 0; i < this.obstacles.length; i++) {
      const obs = this.obstacles[i];
      obs.x -= this.speed;
      
      // Check collision
      if (
        this.dino.x < obs.x + obs.width &&
        this.dino.x + this.dino.width > obs.x &&
        this.dino.y < obs.y + obs.height &&
        this.dino.y + this.dino.height > obs.y
      ) {
        this.gameOver = true;
      }
      
      // Remove off-screen obstacles
      if (obs.x + obs.width < 0) {
        this.obstacles.splice(i, 1);
        i--;
        this.score++;
      }
    }
    
    // Increase speed over time
    if (this.score > 0 && this.score % 5 === 0) {
      this.speed = 5 + Math.floor(this.score / 5);
    }
  }
  
  render() {
    // Clear canvas
    this.ctx.clearRect(0, 0, this.width, this.height);
    
    // Draw ground
    this.ctx.beginPath();
    this.ctx.moveTo(0, 180);
    this.ctx.lineTo(this.width, 180);
    this.ctx.stroke();
    
    // Draw dino
    this.ctx.fillRect(this.dino.x, this.dino.y, this.dino.width, this.dino.height);
    
    // Draw obstacles
    for (const obs of this.obstacles) {
      this.ctx.fillRect(obs.x, obs.y, obs.width, obs.height);
    }
    
    // Draw score
    this.ctx.font = '20px Arial';
    this.ctx.fillText(`Score: ${this.score}`, 20, 30);
    
    // Game over screen
    if (this.gameOver) {
      this.ctx.fillStyle = 'rgba(0, 0, 0, 0.5)';
      this.ctx.fillRect(0, 0, this.width, this.height);
      
      this.ctx.fillStyle = 'white';
      this.ctx.font = '40px Arial';
      this.ctx.fillText('Game Over', this.width / 2 - 100, this.height / 2);
      
      this.ctx.font = '20px Arial';
      this.ctx.fillText('Press Space to restart', this.width / 2 - 100, this.height / 2 + 40);
    }
  }
  
  mainLoop() {
    if (!this.gameOver) {
      this.update();
    }
    
    this.render();
    requestAnimationFrame(this.mainLoop.bind(this));
  }
  
  reset() {
    this.dino = { x: 50, y: 150, width: 40, height: 60, jumping: false, yVelocity: 0 };
    this.obstacles = [];
    this.score = 0;
    this.speed = 5;
    this.gameOver = false;
  }
}

// Start game
window.onload = () => {
  new Game();
};
```

<p align="center">To play the full game, visit <a href="https://eyestore.tebex.io/">my Tebex store</a> and check out my interactive UI scripts!</p>
</details>

<!-- Stats Section -->
<div align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=raiderss&show_icons=true&theme=radical&hide_border=true&custom_title=The%20Raider%27s%20GitHub%20Stats" alt="GitHub Stats" height="170"/>
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=raiderss&theme=radical&hide_border=true" alt="GitHub Streak" height="170"/>
</div>

<br>

<!-- Projects Section -->
<h2 align="center">🏆 Featured FiveM Scripts</h2>

<table>
  <tr>
    <td align="center" width="33%">
      <a href="https://github.com/raiderss/es-antidump">
        <img src="https://img.shields.io/badge/ES--ANTIDUMP-Security-FF5700?style=for-the-badge&logo=shield&logoColor=white" alt="ES-ANTIDUMP"/>
      </a>
      <p>Advanced protection against script dumping</p>
    </td>
    <td align="center" width="33%">
      <a href="https://github.com/raiderss/FYAC">
        <img src="https://img.shields.io/badge/FYAC-Anticheat-FF0000?style=for-the-badge&logo=shield&logoColor=white" alt="FYAC"/>
      </a>
      <p>Premium FiveM anticheat solution</p>
    </td>
    <td align="center" width="33%">
      <a href="https://github.com/raiderss/es-alphahud">
        <img src="https://img.shields.io/badge/ES--ALPHAHUD-Interface-00C4CC?style=for-the-badge&logo=html5&logoColor=white" alt="ES-ALPHAHUD"/>
      </a>
      <p>Modern HUD system for FiveM</p>
    </td>
  </tr>
  <tr>
    <td align="center" width="33%">
      <a href="https://github.com/raiderss/qb-inventory">
        <img src="https://img.shields.io/badge/QB--INVENTORY-UI-4C8EDA?style=for-the-badge&logo=react&logoColor=white" alt="QB-INVENTORY"/>
      </a>
      <p>Enhanced inventory UI for QBCore</p>
    </td>
    <td align="center" width="33%">
      <a href="https://github.com/raiderss/es-jobcenter">
        <img src="https://img.shields.io/badge/ES--JOBCENTER-Economy-2ECC71?style=for-the-badge&logo=cash-app&logoColor=white" alt="ES-JOBCENTER"/>
      </a>
      <p>Advanced job management system</p>
    </td>
    <td align="center" width="33%">
      <a href="https://github.com/raiderss/es-emotemenu">
        <img src="https://img.shields.io/badge/ES--EMOTEMENU-Animation-9B59B6?style=for-the-badge&logo=gamepad&logoColor=white" alt="ES-EMOTEMENU"/>
      </a>
      <p>Extensive animation system</p>
    </td>
  </tr>
</table>

<!-- Categories -->
<details>
  <summary>
    <h3 align="center">🔐 Security & Protection Systems</h3>
  </summary>
  <ul>
    <li><a href="https://github.com/raiderss/es-antidump">ES-ANTIDUMP</a> - Script theft protection</li>
    <li><a href="https://github.com/raiderss/es-antibackdoor">ES-ANTIBACKDOOR</a> - Backdoor protection</li>
    <li><a href="https://github.com/raiderss/FYAC">FYAC</a> - Anti-cheat system</li>
  </ul>
</details>

<details>
  <summary>
    <h3 align="center">🎮 UI/UX & Frameworks</h3>
  </summary>
  <ul>
    <li><a href="https://github.com/raiderss/es-alphahud">ES-ALPHAHUD</a> - Modern HUD system</li>
    <li><a href="https://github.com/raiderss/qb-inventory">QB-INVENTORY</a> - Enhanced inventory</li>
    <li><a href="https://github.com/raiderss/eyes-store-game-ui-template">GAME-UI-TEMPLATE</a> - Website templates</li>
    <li><a href="https://github.com/raiderss/qb-multicharacter">QB-MULTICHARACTER</a> - Character system</li>
  </ul>
</details>

<details>
  <summary>
    <h3 align="center">🚗 Vehicle & Economy Systems</h3>
  </summary>
  <ul>
    <li><a href="https://github.com/raiderss/es-garage">ES-GARAGE</a> - Vehicle management</li>
    <li><a href="https://github.com/raiderss/es-jobcenter">ES-JOBCENTER</a> - Employment system</li>
    <li><a href="https://github.com/raiderss/es-rentacar">ES-RENTACAR</a> - Vehicle rental system</li>
  </ul>
</details>

<details>
  <summary>
    <h3 align="center">🎯 Utilities & Gameplay</h3>
  </summary>
  <ul>
    <li><a href="https://github.com/raiderss/es-emotemenu">ES-EMOTEMENU</a> - Animation system</li>
    <li><a href="https://github.com/raiderss/es-treasure">ES-TREASURE</a> - Looting system</li>
    <li><a href="https://github.com/raiderss/es-coords">ES-COORDS</a> - Developer tools</li>
    <li><a href="https://github.com/raiderss/es-tattoos">ES-TATTOOS</a> - Tattoo system</li>
  </ul>
</details>

<!-- Contact Section -->
<h2 align="center">📫 Connect With Me</h2>

<div align="center">
  <a href="https://discord.gg/EkwWvFS">
    <img src="https://img.shields.io/badge/Discord-Join_Our_Community-5865F2?style=for-the-badge&logo=discord&logoColor=white"/>
  </a>
  <a href="https://eyestore.tebex.io/">
    <img src="https://img.shields.io/badge/Tebex-Premium_Scripts-00A2FF?style=for-the-badge&logo=shopify&logoColor=white"/>
  </a>
  <a href="https://www.youtube.com/channel/UCw11VeGY4MFKItj0FGm7FUQ">
    <img src="https://img.shields.io/badge/YouTube-Script_Showcases-FF0000?style=for-the-badge&logo=youtube&logoColor=white"/>
  </a>
</div>

<!-- Footer -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer" width="100%"/>

<!--
SEO KEYWORDS:
fivem developer, fivem script creator, fivem freelancer, qbcore developer, esx developer,
fivem ui designer, lua programmer, fivem scripts, fivem security, premium fivem scripts,
fivem shop system, fivem custom scripts, fivem roleplay scripts, qbcore scripts, esx scripts,
fivem resource developer, fivem expert, fivem consultant, fiveM programming, fivem job system
-->