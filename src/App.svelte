<script>
  import { onMount } from "svelte";

  let activeSection = "hero";
  let currentQuote = 0;
  let currentFact = 0;
  let coinFlipped = true;
  let isPlaying = false;
  let audioElement;
  let roadmapVisible = [false, false, false, false];

  const quotes = [
    "Success comes from dedication and superior genetics",
    "The path to victory requires discipline and beet farming",
    "Bears, beets, blockchain - the pillars of prosperity",
    "Whenever I'm about to do something, I think 'Would an idiot do that?' And if they would, I do not do that thing",
    "I am faster than 80% of all snakes",
    "Through concentration, I can raise and lower my cholesterol at will",
    "In the end, the greatest snowball isn't a snowball at all. It's fear",
  ];

  const dwightFacts = [
    "🥋 Black belt in Goju-Ryu karate",
    "👮 Volunteer Sheriff's Deputy",
    "🥬 Beet Farm Owner & Operator",
    "📊 Salesman of the Year",
    "🏃 Can run a sub-6 minute mile",
    "🎯 Expert marksman",
    "🐻 Survived a bear attack",
  ];

  const roadmapPhases = [
    {
      phase: "Phase 1",
      title: "Launch",
      status: "✅",
      description: "Fair launch on blockchain. LP burned. Renounced.",
      icon: "🚀",
    },
    {
      phase: "Phase 2",
      title: "Community Building",
      status: "🔄",
      description: "Grow the Schrute Army. Partnerships with beet farms.",
      icon: "🥬",
    },
    {
      phase: "Phase 3",
      title: "Schrute Farms NFTs",
      status: "📋",
      description: "Limited edition Schrute Farms NFT collection.",
      icon: "🖼️",
    },
    {
      phase: "Phase 4",
      title: "World Domination",
      status: "🎯",
      description: "Schrute Bucks become the only currency that matters.",
      icon: "🌍",
    },
  ];

  const whyCards = [
    {
      title: "Battle-Tested",
      icon: "⚔️",
      front: "Forged in the fires of Schrute Farms",
      back: "Built on principles of strength, honor, and superior intelligence",
    },
    {
      title: "Asset-Backed",
      icon: "🥬",
      front: "Secured by premium beet farm holdings",
      back: "Real agricultural value backing every token",
    },
    {
      title: "Zero Nonsense",
      icon: "🛡️",
      front: "No tolerance for paper hands",
      back: "Community of dedicated warriors and true believers",
    },
    {
      title: "Proven Leadership",
      icon: "👔",
      front: "Led by Assistant Regional Manager principles",
      back: "Decades of excellence in paper sales translate to crypto dominance",
    },
  ];

  const socials = [
    { name: "Twitter", url: "https://x.com/DunderMifflinD", icon: "𝕏" },
    { name: "Telegram", url: "https://t.me/+8rF5hBkmkdphNzQ8", icon: "✈️" },
    { name: "Discord", url: "#", icon: "💬" },
  ];

  function scrollToSection(section) {
    const element = document.getElementById(section);
    if (element) {
      element.scrollIntoView({ behavior: "smooth" });
    }
  }

  function flipCoin() {
    coinFlipped = !coinFlipped;
  }

  function toggleMusic() {
    if (!audioElement) return;

    if (isPlaying) {
      audioElement.pause();
    } else {
      audioElement.play();
    }
    isPlaying = !isPlaying;
  }

  function handleScroll() {
    const roadmapSection = document.getElementById("roadmap");
    if (!roadmapSection) return;

    const sectionTop = roadmapSection.offsetTop;
    const sectionHeight = roadmapSection.offsetHeight;
    const scrollPosition = window.scrollY + window.innerHeight;

    roadmapPhases.forEach((_, index) => {
      const triggerPoint =
        sectionTop + (sectionHeight / roadmapPhases.length) * index;
      if (scrollPosition > triggerPoint + 100) {
        roadmapVisible[index] = true;
      }
    });
    roadmapVisible = [...roadmapVisible];
  }

  onMount(() => {
    const quoteInterval = setInterval(() => {
      currentQuote = (currentQuote + 1) % quotes.length;
    }, 5000);

    const factInterval = setInterval(() => {
      currentFact = (currentFact + 1) % dwightFacts.length;
    }, 3000);

    window.addEventListener("scroll", handleScroll);
    handleScroll();

    return () => {
      clearInterval(quoteInterval);
      clearInterval(factInterval);
      window.removeEventListener("scroll", handleScroll);
    };
  });
</script>

<main>
  <div class="music-toggle">
    <p class="anthem-label">Beet Anthem</p>
    <button
      class="music-btn"
      on:click={toggleMusic}
      aria-label="Toggle Beet Anthem"
    >
      {#if isPlaying}
        🔊
      {:else}
        🔇
      {/if}
    </button>
  </div>

  <!-- Hidden audio element -->
  <audio bind:this={audioElement} loop>
    <source src="/audio/Schrute Bucks Anthem.mp3" type="audio/mpeg" />
  </audio>

  <nav>
    <div class="nav-container">
      <div
        class="nav-brand"
        on:click={() => scrollToSection("hero")}
        on:keypress={(e) => e.key === "Enter" && scrollToSection("hero")}
        role="button"
        tabindex="0"
        aria-label="Go to home"
      >
        <img
          src="/img/DwightCoin-Only.png"
          alt="Schrute Bucks Logo"
          class="nav-logo"
        />
        <div class="logo">$CHRUTE BUCKS</div>
      </div>
      <div class="nav-links">
        <button on:click={() => scrollToSection("about")}>About</button>
        <button on:click={() => scrollToSection("why")}>Why</button>
        <button on:click={() => scrollToSection("roadmap")}>Roadmap</button>
        <button on:click={() => scrollToSection("media")}>Media</button>
        <button on:click={() => scrollToSection("tokenomics")}
          >Tokenomics</button
        >
        <button on:click={() => scrollToSection("socials")}>Socials</button>
      </div>
    </div>
  </nav>

  <section id="hero" class="hero">
    <div class="hero-content">
      <h1 class="glitch" data-text="SCHRUTE BUCKS">SCHRUTE BUCKS</h1>
      <p class="subtitle">The Only Currency That Matters</p>
      <p class="tagline">"In Dwight We Trust"</p>
      <div class="hero-buttons">
        <a
          href="https://join.pump.fun/HSag/030q6eod"
          target="_blank"
          rel="noopener noreferrer"
          class="btn-primary"
        >
          PUMP Beets Now!
        </a>
        <button class="btn-secondary" on:click={() => scrollToSection("about")}
          >Learn More</button
        >
      </div>
    </div>
    <div class="hero-image">
      <div
        class="coin-container"
        class:flipped={coinFlipped}
        on:click={flipCoin}
        on:keypress={(e) => e.key === "Enter" && flipCoin()}
        role="button"
        tabindex="0"
        aria-label="Click to flip coin"
      >
        <div class="coin">
          <div class="coin-front">
            <img src="/img/DwightCoin-Only.png" alt="Schrute Bucks" />
          </div>
          <div class="coin-back">
            <div class="moon-text">
              To the<br />Mooooon!
              <div class="rocket">🚀</div>
            </div>
          </div>
        </div>
      </div>
      <p class="coin-hint">👆 Click the coin!</p>
    </div>
  </section>

  <!-- Quote Carousel -->
  <section class="quotes-section">
    <div class="container">
      <div class="quote-carousel">
        {#each quotes as quote, i}
          <div class="quote" class:active={i === currentQuote}>
            <span class="quote-mark">"</span>
            {quote}
            <span class="quote-mark">"</span>
            <p class="quote-author">- Dwight Schrute</p>
          </div>
        {/each}
      </div>
      <div class="quote-dots">
        {#each quotes as _, i}
          <button
            class="dot"
            class:active={i === currentQuote}
            on:click={() => (currentQuote = i)}
          ></button>
        {/each}
      </div>
    </div>
  </section>

  <!-- Dwight Facts Banner -->
  <section class="facts-banner">
    <div class="facts-container">
      <p>Why Dwight will lead us to victory?</p>
      {#each dwightFacts as fact, i}
        <div class="fact" class:active={i === currentFact}>
          {fact}
        </div>
      {/each}
    </div>
  </section>

  <!-- Why Schrute Bucks Section -->
  <section id="why" class="why-section">
    <div class="container">
      <h2>Why Schrute Bucks?</h2>
      <div class="why-grid">
        {#each whyCards as card}
          <div class="flip-card">
            <div class="flip-card-inner">
              <div class="flip-card-front">
                <div class="card-icon">{card.icon}</div>
                <h3>{card.title}</h3>
                <p>{card.front}</p>
              </div>
              <div class="flip-card-back">
                <p>{card.back}</p>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <section id="about" class="about">
    <div class="container">
      <h2>What Are Schrute Bucks?</h2>
      <div class="about-content">
        <p>
          Schrute Bucks are the revolutionary memecoin inspired by the greatest
          Assistant Regional Manager in paper sales history. Built on the
          principles of beet farming, martial arts excellence, and superior
          intelligence.
        </p>
        <p>
          This isn't just a memecoin. It's a movement. It's a lifestyle. It's
          IDENTITY THEFT.
        </p>
        <div class="stats">
          <div class="stat">
            <h3>1,000,000,000</h3>
            <p>Total Supply</p>
          </div>
          <div class="stat">
            <h3>0%</h3>
            <p>Tax</p>
          </div>
          <div class="stat">
            <h3>100%</h3>
            <p>Community</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ROADMAP SECTION -->
  <section id="roadmap" class="roadmap">
    <div class="container">
      <h2>The Path to Greatness</h2>
      <div class="roadmap-timeline">
        {#each roadmapPhases as phase, index}
          <div class="roadmap-item" class:visible={roadmapVisible[index]}>
            <div class="roadmap-icon">{phase.icon}</div>
            <div class="roadmap-content">
              <div class="roadmap-phase">{phase.phase}</div>
              <h3>{phase.title} {phase.status}</h3>
              <p>{phase.description}</p>
            </div>
            {#if index < roadmapPhases.length - 1}
              <div class="roadmap-line"></div>
            {/if}
          </div>
        {/each}
      </div>
    </div>
  </section>

  <section id="media" class="media">
    <div class="container">
      <h2>Memes & Media</h2>
      <div class="media-grid">
        <div class="media-item">
          <video
            on:mouseenter={(e) => e.currentTarget.play()}
            on:mouseleave={(e) => {
              e.currentTarget.pause();
              e.currentTarget.currentTime = 0;
            }}
            loop
          >
            <source src="video/SchruteVID.mp4" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
        </div>
        <div class="media-item">
          <img src="/img/DwightCoin-Only.png" alt="Schrute Bucks Logo" />
        </div>
      </div>
    </div>
  </section>

  <section id="tokenomics" class="tokenomics">
    <div class="container">
      <h2>Tokenomics</h2>
      <div class="tokenomics-content">
        <div class="token-item">
          <h3>📊 Supply</h3>
          <p>1,000,000,000 $CHRUTE</p>
        </div>
        <div class="token-item">
          <h3>🔥 Burned</h3>
          <p>LP Burned Forever</p>
        </div>
        <div class="token-item">
          <h3>💎 Distribution</h3>
          <p>100% Fair Launch</p>
        </div>
        <div class="token-item">
          <h3>⚡ Conversion Rate</h3>
          <p>1 Schrute Buck = 0.0001 Stanley Nickels</p>
        </div>
      </div>
    </div>
  </section>

  <section id="socials" class="socials">
    <div class="container">
      <h2>Join The Beet Farm</h2>
      <div class="social-links">
        {#each socials as social}
          <a
            href={social.url}
            target="_blank"
            rel="noopener noreferrer"
            class="social-btn"
          >
            <span class="social-icon">{social.icon}</span>
            <span>{social.name}</span>
          </a>
        {/each}
      </div>
      <div class="contract">
        <p>Grow your beet farm below</p>
        <code>vquGSV4ocqUHN2Qrci2aHkhGsvsH2ciewq9C7dMKjv9</code>
      </div>
    </div>
  </section>

  <footer>
    <p>© 2024 Schrute Bucks. All rights reserved. Bears. Beets. Blockchain.</p>
    <p class="disclaimer">This is a memecoin. DYOR. Not financial advice.</p>
  </footer>
</main>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family:
      "Inter",
      -apple-system,
      BlinkMacSystemFont,
      "Segoe UI",
      sans-serif;
    background: #0a0a0a;
    color: #ffffff;
    overflow-x: hidden;
  }

  .music-toggle {
    position: fixed;
    bottom: 2rem;
    right: 2rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    z-index: 1001;
  }

  .anthem-label {
    color: #ffd700;
    font-size: 0.8rem;
    font-weight: 600;
    letter-spacing: 1px;
    opacity: 0.8;
    animation: fadeInOut 2s ease-in-out infinite alternate;
    margin: 0;
    text-align: center;
  }

  @keyframes fadeInOut {
    from {
      opacity: 0.6;
    }
    to {
      opacity: 0.9;
    }
  }

  .music-btn {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    border: none;
    font-size: 1.8rem;
    cursor: pointer;
    box-shadow: 0 4px 20px rgba(255, 215, 0, 0.4);
    transition: all 0.3s;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative; /* Changed from fixed—now stacks in toggle */
  }

  .music-btn:hover {
    transform: scale(1.1);
    box-shadow: 0 6px 30px rgba(255, 215, 0, 0.6);
  }

  nav {
    position: fixed;
    top: 0;
    width: 100%;
    background: rgba(10, 10, 10, 0.95);
    backdrop-filter: blur(10px);
    z-index: 1000;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .nav-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 1rem 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
  }

  .nav-brand {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
    transition: opacity 0.3s ease;
  }

  .nav-brand:hover {
    opacity: 0.8;
    .logo {
      color: #ffd700;
    }
  }

  .nav-logo {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    object-fit: cover;
    transition: transform 0.3s ease;
  }

  .nav-brand:hover .nav-logo {
    transform: scale(1.1);
  }

  .logo {
    font-size: 1.5rem;
    font-weight: 900;
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    background-clip: text;
    letter-spacing: 2px;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
  }

  .nav-links button {
    background: none;
    border: none;
    color: #ffffff;
    cursor: pointer;
    font-size: 1rem;
    transition: color 0.3s;
  }

  .nav-links button:hover {
    color: #ffd700;
  }

  .hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 6rem 2rem 2rem;
    max-width: 1200px;
    margin: 0 auto;
    gap: 4rem;
  }

  .hero-content {
    flex: 1;
  }

  .glitch {
    font-size: 4rem;
    font-weight: 900;
    margin: 0;
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: glow 2s ease-in-out infinite alternate;
  }

  @keyframes glow {
    from {
      filter: drop-shadow(0 0 20px rgba(255, 215, 0, 0.5));
    }
    to {
      filter: drop-shadow(0 0 40px rgba(255, 215, 0, 0.8));
    }
  }

  .subtitle {
    font-size: 1.5rem;
    margin: 1rem 0;
    color: #cccccc;
  }

  .tagline {
    font-size: 1.2rem;
    font-style: italic;
    color: #888888;
    margin-bottom: 2rem;
  }

  .hero-buttons {
    display: flex;
    gap: 1rem;
  }

  .btn-primary,
  .btn-secondary {
    padding: 1rem 2rem;
    font-size: 1.1rem;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-weight: 600;
    transition: all 0.3s;
  }

  .btn-primary {
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    color: #000000;
  }

  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 30px rgba(255, 215, 0, 0.4);
  }

  .btn-secondary {
    background: transparent;
    border: 2px solid #ffd700;
    color: #ffd700;
  }

  .btn-secondary:hover {
    background: rgba(255, 215, 0, 0.1);
  }

  .hero-image {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }

  /* FLIPPING COIN - FIXED VERSION */
  .coin-container {
    perspective: 1000px;
    cursor: pointer;
    width: 400px;
    height: 400px;
  }

  .coin {
    position: relative;
    width: 100%;
    height: 100%;
    transition: transform 0.8s;
    transform-style: preserve-3d;
  }

  .coin-container.flipped .coin {
    transform: rotateY(180deg);
  }

  .coin-front {
    position: absolute;
    width: 100%;
    height: 100%;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background: transparent;
    box-shadow: 0 0 50px rgba(255, 215, 0, 0.5);
    animation: float 3s ease-in-out infinite;
    transform: rotateY(0deg); /* Make sure front is not rotated */
  }

  .coin-front img {
    width: 95%;
    height: 95%;
    object-fit: cover;
    border-radius: 50%;
    filter: drop-shadow(0 0 30px rgba(255, 215, 0, 0.6));
    transform: scaleX(-1); /* FLIP THE IMAGE HORIZONTALLY */
  }

  .coin-back {
    position: absolute;
    width: 100%;
    height: 100%;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background: radial-gradient(circle at 30% 30%, #ffd700, #b8860b);
    box-shadow: 0 0 50px rgba(255, 215, 0, 0.5);
    transform: rotateY(180deg);
    animation: float 3s ease-in-out infinite;
    backface-visibility: hidden;
  }

  .moon-text {
    font-size: 3rem;
    font-weight: 900;
    color: #000;
    text-align: center;
    line-height: 1.2;
    text-shadow: 2px 2px 4px rgba(255, 255, 255, 0.3);
  }

  .rocket {
    font-size: 4rem;
    margin-top: 1rem;
    animation: rocketBounce 1s ease-in-out infinite;
  }

  @keyframes rocketBounce {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-20px);
    }
  }

  @keyframes float {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-20px);
    }
  }

  .coin-hint {
    color: #888;
    font-size: 0.9rem;
    animation: pulse 2s ease-in-out infinite;
  }

  @keyframes pulse {
    0%,
    100% {
      opacity: 0.5;
    }
    50% {
      opacity: 1;
    }
  }

  .quotes-section {
    padding: 4rem 2rem;
    background: linear-gradient(180deg, #0a0a0a 0%, #1a1a1a 100%);
  }

  .quote-carousel {
    position: relative;
    min-height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .quote {
    position: absolute;
    max-width: 800px;
    text-align: center;
    font-size: 1.8rem;
    font-style: italic;
    color: #ffffff;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.8s ease;
    pointer-events: none;
  }

  .quote.active {
    opacity: 1;
    transform: translateY(0);
    pointer-events: auto;
  }

  .quote-mark {
    color: #ffd700;
    font-size: 3rem;
    font-family: Georgia, serif;
  }

  .quote-author {
    margin-top: 1rem;
    font-size: 1.2rem;
    color: #ffd700;
    font-style: normal;
  }

  .quote-dots {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 3rem;
  }

  .dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: rgba(255, 215, 0, 0.3);
    border: none;
    cursor: pointer;
    transition: all 0.3s;
  }

  .dot.active {
    background: #ffd700;
    transform: scale(1.3);
  }

  /* DWIGHT FACTS BANNER */
  .facts-banner {
    background: linear-gradient(90deg, #ffd700, #ffed4e, #ffd700);
    padding: 1.5rem 2rem;
    overflow: hidden;
    position: relative;
  }

  .facts-container {
    position: relative;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;

    p{
              position: absolute;
        bottom: 0;
      font-size: 1.5rem;
      font-weight: 700;
      color: #000;
      margin-right: 2rem;
      white-space: nowrap;
      font-family: math;
    }
  }

  .fact {
    position: absolute;
    font-size: 1.3rem;
    font-weight: 700;
    color: #000;
    white-space: nowrap;
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.5s ease;
  }

  .fact.active {
    opacity: 1;
    transform: translateY(0);
    padding-top: 25px;
  }

  /* WHY SECTION - FLIP CARDS */
  .why-section {
    padding: 5rem 2rem;
    background: #0a0a0a;
  }

  .why-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    margin-top: 3rem;
  }

  .flip-card {
    height: 300px;
    perspective: 1000px;
  }

  .flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    transition: transform 0.6s;
    transform-style: preserve-3d;
  }

  .flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
  }

  .flip-card-front,
  .flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
    border-radius: 12px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
  }

  .flip-card-front {
    background: linear-gradient(
      135deg,
      rgba(255, 215, 0, 0.1),
      rgba(255, 215, 0, 0.05)
    );
    border: 2px solid rgba(255, 215, 0, 0.3);
  }

  .flip-card-back {
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    color: #000;
    transform: rotateY(180deg);
  }

  .card-icon {
    font-size: 4rem;
    margin-bottom: 1rem;
  }

  .flip-card-front h3 {
    font-size: 1.5rem;
    color: #ffd700;
    margin-bottom: 1rem;
  }

  .flip-card-front p {
    color: #cccccc;
    font-size: 1rem;
  }

  .flip-card-back p {
    font-size: 1.1rem;
    font-weight: 600;
    line-height: 1.6;
  }

  /* ROADMAP SECTION */
  .roadmap {
    padding: 5rem 2rem;
    background: linear-gradient(180deg, #0a0a0a 0%, #1a1a1a 100%);
  }

  .roadmap-timeline {
    max-width: 800px;
    margin: 0 auto;
    position: relative;
  }

  .roadmap-item {
    display: flex;
    gap: 2rem;
    margin-bottom: 4rem;
    position: relative;
    opacity: 0;
    transform: translateX(-50px);
    transition: all 0.6s ease;
  }

  .roadmap-item.visible {
    opacity: 1;
    transform: translateX(0);
  }

  .roadmap-icon {
    font-size: 3rem;
    min-width: 80px;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    border-radius: 50%;
    box-shadow: 0 4px 20px rgba(255, 215, 0, 0.4);
    flex-shrink: 0;
  }

  .roadmap-content {
    flex: 1;
  }

  .roadmap-phase {
    color: #ffd700;
    font-size: 0.9rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-bottom: 0.5rem;
  }

  .roadmap-content h3 {
    font-size: 1.8rem;
    color: #ffffff;
    margin: 0 0 1rem 0;
  }

  .roadmap-content p {
    color: #cccccc;
    line-height: 1.6;
  }

  .roadmap-line {
    position: absolute;
    left: 40px;
    top: 80px;
    width: 2px;
    height: 100%;
    background: linear-gradient(180deg, #ffd700, transparent);
  }

  section {
    padding: 5rem 2rem;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  h2 {
    font-size: 3rem;
    text-align: center;
    margin-bottom: 3rem;
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    background-clip: text;
  }

  .about {
    background: linear-gradient(180deg, #0a0a0a 0%, #1a1a1a 100%);
  }

  .about-content p {
    font-size: 1.2rem;
    line-height: 1.8;
    color: #cccccc;
    margin-bottom: 1.5rem;
  }

  .stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2rem;
    margin-top: 3rem;
  }

  .stat {
    text-align: center;
    padding: 2rem;
    background: rgba(255, 215, 0, 0.05);
    border: 1px solid rgba(255, 215, 0, 0.2);
    border-radius: 12px;
  }

  .stat h3 {
    font-size: 2.5rem;
    color: #ffd700;
    margin: 0;
  }

  .stat p {
    color: #888888;
    margin-top: 0.5rem;
  }

  .media-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }

  .media-item {
    aspect-ratio: 1;
    border-radius: 12px;
    overflow: hidden;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    transition: transform 0.3s;
  }

  .media-item video {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 12px;
  }

  .media-item:hover {
    transform: scale(1.05);
  }

  .tokenomics {
    background: linear-gradient(180deg, #0a0a0a 0%, #1a1a1a 100%);
  }

  .tokenomics-content {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
  }

  .token-item {
    text-align: center;
    padding: 2rem;
    background: rgba(255, 215, 0, 0.05);
    border: 1px solid rgba(255, 215, 0, 0.2);
    border-radius: 12px;
  }

  .token-item h3 {
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  .token-item p {
    color: #cccccc;
    font-size: 1.1rem;
  }

  .social-links {
    display: flex;
    justify-content: center;
    gap: 2rem;
    flex-wrap: wrap;
  }

  .social-btn {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 1rem 2rem;
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    color: #000000;
    text-decoration: none;
    border-radius: 8px;
    font-weight: 600;
    transition: all 0.3s;
  }

  .social-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 30px rgba(255, 215, 0, 0.4);
  }

  .social-icon {
    font-size: 1.5rem;
  }

  .contract {
    margin-top: 3rem;
    text-align: center;
  }

  .contract p {
    color: #888888;
    margin-bottom: 0.5rem;
  }

  .contract code {
    background: rgba(255, 215, 0, 0.1);
    padding: 1rem 2rem;
    border-radius: 8px;
    color: #ffd700;
    font-size: 1.1rem;
    display: inline-block;
  }

  footer {
    text-align: center;
    padding: 3rem 2rem;
    background: #050505;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
  }

  footer p {
    color: #666666;
    margin: 0.5rem 0;
  }

  .disclaimer {
    font-size: 0.9rem;
    font-style: italic;
  }

  @media (max-width: 768px) {
    .hero {
      flex-direction: column;
      text-align: center;
    }

    .glitch {
      font-size: 2.5rem;
    }

    .nav-links {
      gap: 0.5rem;
      flex-wrap: wrap;
      justify-content: center;
    }

    .nav-links button {
      font-size: 0.85rem;
    }

    .coin-container {
      width: 300px;
      height: 300px;
    }

    .moon-text {
      font-size: 2rem;
    }

    .rocket {
      font-size: 3rem;
    }

    h2 {
      font-size: 2rem;
    }

    .quote {
      font-size: 1.3rem;
      padding: 0 1rem;
    }

    .fact {
      font-size: 1rem;
    }

    .roadmap-item {
      flex-direction: column;
      gap: 1rem;
    }

    .roadmap-line {
      display: none;
    }

    .music-btn {
      width: 50px;
      height: 50px;
      font-size: 1.5rem;
    }

    .anthem-label {
      font-size: 0.7rem; /* Slightly smaller on mobile for fit */
    }
  }
</style>
