<script>
  import { onMount } from 'svelte';

  let activeSection = 'hero';

  const socials = [
    { name: 'Twitter', url: '#', icon: '𝕏' },
    { name: 'Telegram', url: '#', icon: '✈️' },
    { name: 'Discord', url: '#', icon: '💬' },
  ];

  const media = [
    { type: 'video', url: 'your-video-url.mp4', thumb: 'thumbnail.jpg' },
    { type: 'image', url: 'meme1.jpg' },
    { type: 'image', url: 'meme2.jpg' },
  ];

  function scrollToSection(section) {
    const element = document.getElementById(section);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  }
</script>

<main>
  <nav>
    <div class="nav-container">
      <div class="logo">$CHRUTE BUCKS</div>
      <div class="nav-links">
        <button on:click={() => scrollToSection('about')}>About</button>
        <button on:click={() => scrollToSection('media')}>Media</button>
        <button on:click={() => scrollToSection('tokenomics')}>Tokenomics</button>
        <button on:click={() => scrollToSection('socials')}>Socials</button>
      </div>
    </div>
  </nav>

  <section id="hero" class="hero">
    <div class="hero-content">
      <h1 class="glitch" data-text="SCHRUTE BUCKS">SCHRUTE BUCKS</h1>
      <p class="subtitle">The Only Currency That Matters</p>
      <p class="tagline">"In Dwight We Trust"</p>
      <div class="hero-buttons">
        <button class="btn-primary">Buy Now</button>
        <button class="btn-secondary" on:click={() => scrollToSection('about')}>Learn More</button>
      </div>
    </div>
    <div class="hero-image">
      <div class="placeholder-img">🥇</div>
    </div>
  </section>

  <section id="about" class="about">
    <div class="container">
      <h2>What Are Schrute Bucks?</h2>
      <div class="about-content">
        <p>
          Schrute Bucks are the revolutionary memecoin inspired by the greatest Assistant 
          Regional Manager in paper sales history. Built on the principles of beet farming, 
          martial arts excellence, and superior intelligence.
        </p>
        <p>
          This isn't just a memecoin. It's a movement. It's a lifestyle. It's IDENTITY THEFT.
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

  <section id="media" class="media">
    <div class="container">
      <h2>Memes & Media</h2>
      <div class="media-grid">
        <div class="media-item">
          <div class="placeholder-media">Video 1</div>
        </div>
        <div class="media-item">
          <div class="placeholder-media">Meme 1</div>
        </div>
        <div class="media-item">
          <div class="placeholder-media">Meme 2</div>
        </div>
        <div class="media-item">
          <div class="placeholder-media">Video 2</div>
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
          <a href={social.url} target="_blank" rel="noopener noreferrer" class="social-btn">
            <span class="social-icon">{social.icon}</span>
            <span>{social.name}</span>
          </a>
        {/each}
      </div>
      <div class="contract">
        <p>Contract Address:</p>
        <code>0x123...YOUR_CONTRACT_HERE</code>
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
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: #0a0a0a;
    color: #ffffff;
    overflow-x: hidden;
  }

  * {
    box-sizing: border-box;
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
  }

  .logo {
    font-size: 1.5rem;
    font-weight: 900;
    background: linear-gradient(135deg, #ffd700, #ffed4e);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
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
    from { filter: drop-shadow(0 0 20px rgba(255, 215, 0, 0.5)); }
    to { filter: drop-shadow(0 0 40px rgba(255, 215, 0, 0.8)); }
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

  .btn-primary, .btn-secondary {
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
    justify-content: center;
    align-items: center;
  }

  .placeholder-img {
    font-size: 15rem;
    animation: float 3s ease-in-out infinite;
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
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
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
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

  .media-item:hover {
    transform: scale(1.05);
  }

  .placeholder-media {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5rem;
    color: #666666;
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
      gap: 1rem;
    }

    .nav-links button {
      font-size: 0.9rem;
    }

    .placeholder-img {
      font-size: 8rem;
    }

    h2 {
      font-size: 2rem;
    }
  }
</style>