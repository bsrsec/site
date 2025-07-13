<script>

    import config from './config.js'

    let isOpen = false;
  
    function scrollToSection(id) {
      const el = document.getElementById(id);
      if (el) {
        el.scrollIntoView({ behavior: 'smooth' });
        isOpen = false;
      }
    }

    import { fly } from 'svelte/transition';
  import { onMount } from 'svelte';

  let showImage = false;
  let showText1 = false;
  let showText2 = false;

  onMount(() => {
    setTimeout(() => showImage = true, 100);
    setTimeout(() => showText1 = true, 600);
    setTimeout(() => showText2 = true, 1000);
  });

  
  let visible = false;

  function handleIntersect(entries) {
    if (entries[0].isIntersecting) {
      visible = true;
    }
  }

  function observe(node) {
    const observer = new IntersectionObserver(handleIntersect, {
      threshold: 0.2
    });

    observer.observe(node);

    return {
      destroy() {
        observer.unobserve(node);
      }
    };
  }


</script>

  
  <nav>
    <div class="nav-container">
        
        <button on:click={() => scrollToSection('section1')} id="logo" class="logo-grid">
            <img class="logo-img" src="ratlogo.svg" alt="bsr"/>
            <div class="hover-text">
            <span>B</span>
            <span>S</span>
            <span>R</span>
            </div>
      </button>
      <!-- <div class="nav-brand">MySite</div> -->
      <div class="nav-links">
        <button on:click={() => scrollToSection('section1')}>Home</button>
        <button on:click={() => scrollToSection('section2')}>Solutions</button>
        <button on:click={() => scrollToSection('section3')}>Contact</button>
      </div>
      <button class="hamburger" on:click={() => isOpen = !isOpen}>☰</button>
    </div>
    <div class={`mobile-menu ${isOpen ? 'show' : ''}`}>
      <button on:click={() => scrollToSection('section1')}>Home</button>
      <button on:click={() => scrollToSection('section2')}>Solutions</button>
      <button on:click={() => scrollToSection('section3')}>Contact</button>
    </div>
  </nav>
  
  <main style="padding-top: 70px;">
    <section id="section1" class="section">
        <div style="display: flex; flex-direction: column; align-items: center; min-height: 60vh; justify-content:center; ">
            {#if showImage}
              <div transition:fly={{ y: -40, duration: 500 }}>
                <img class="rat" src="rat.svg" alt="Hero Logo" style="transition: transform 0.3s ease; width: 250px; height: auto; margin-bottom: 2rem;" />
              </div>
            {:else}
              <!-- reserve image space -->
              <div style="height: 180px; margin-bottom: 2rem;"></div>
            {/if}
        
            <div style="height: 3.5rem; overflow: hidden;">
              {#if showText1}
                <div transition:fly={{ x: -80, duration: 500 }}>
                  <h1 class="sec1-text" style="margin: 0; color: #6b6c6c;">BSR Cyber Security</h1>
                </div>
              {/if}
            </div>
        
            <div style="height: 2.5rem; overflow: hidden;">
              {#if showText2}
                <div transition:fly={{ x: -80, duration: 500 }}>
                  <p class="sec1-text" style="font-size: 1.3rem; color: #868686; margin: 0;">Cyber Security Consulting and Solutions</p>
                </div>
              {/if}
            </div>
          </div>
    </section>
  
    <section id="section2" class="section">
      <div>
        <!-- <h1>About Us</h1>
        <p>We create user-friendly web experiences using Svelte.</p> -->
        <h2 class="section2-title">Experience clear-cut security with BSR</h2>
        <div class="grid">
            {#each config.solutions as solution}
                <div class="grid-item">
                    <div class="icon-title-grid">
                        <img class="icon" src={solution.icon} alt="">
                        <h2>{solution.title}</h2>
                    </div>
                <p>{solution.content}</p>
                <!-- <button> Expand <i class="arrow right"></i></button> -->
                </div>
            {/each}
        </div>

        <div class="cert-grid">
            <img src="crest-logo.png" alt="" class="cert" />
            <img src="oscplogo.png" alt="" class="cert" />
            <div class="cert cert-item">
                <div style="font-size: 2.5rem">{new Date().getFullYear()-2016}</div>
                <div>years of experience</div>
            </div>
            <!-- <img src="/logos/logo3.png" alt="" class="cert" /> -->
          </div>
        
      </div>
    </section>
  
    <section id="section3" class="section">
        <div use:observe>
            {#if visible}
              <h2 class="section3-title"  transition:fly={{ x: -100, duration: 600, delay: 400 }} >
                Let's get in touch
              </h2>
            {/if}
            
            

            <!-- <h1>Contact</h1> -->
      <!-- <p>Reach us at <i>info@bsrsec.com</i></p> -->
      <div class="container">
        <p class="section3-text">If you have any questions, want to assess your environment, or just want to chat about potential risks — we're here to help.</p>
        <a href="mailto:contact@bsrsec.com" class="email-link">contact@bsrsec.com</a>
        
      </div>
      <!-- <img src="rat.svg" alt="Hero Logo" style="transition: transform 0.3s ease; width: 150px; height: auto; margin-top: 10rem;" /> -->
          </div>
    </section>
  </main>


  
  <style>
    html, body {
      margin: 0;
      padding: 0;
      font-family: system-ui, sans-serif;
      scroll-behavior: smooth;
    }
  
    nav {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      background: #ffffff;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      z-index: 999;
    }
  
    .nav-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      max-width: 1200px;
      margin: 0 auto;
      padding: 1rem;
    }
  
    .nav-brand {
      font-size: 1.5rem;
      font-weight: bold;
      color: #2c3e50;
    }
  
    .nav-links {
      display: flex;
      gap: 1rem;
    }
  
    .nav-links button {
      background: none;
      border: none;
      font-size: 1rem;
      color: #5d5d5e;
      cursor: pointer;
      padding: 0.5rem;
      transition: transform 0.3s ease, color 0.4s ease;
    }
  
    .nav-links button:hover {
        transform: translateY(-5px);
      color: #868686;
    }
  
    .hamburger {
      display: none;
      background: none;
      border: none;
      font-size: 1.5rem;
    }
  
    .mobile-menu {
      display: none;
      flex-direction: column;
      gap: 0.75rem;
      padding: 1rem;
      background: #f8f8f8;
    }
  
    .section {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 2rem;
      text-align: center;
    }
  
    .section h1 {
      font-size: 3rem;
      margin-bottom: 1rem;
    }

    .sec1-text, .sec3-text, .section2-title{
        font-family: "Quicksand";
    }

    .rat:hover{
        transform: scale(1.2);
    }
  
    #section1 {
      background: linear-gradient(to bottom right, #ffffff, #e9e9e9);
      color: white;
    }
  
    #section2 {
      background: #ffffff;
      color: #2c3e50;
      padding-top: 4rem;
    }
  
    #section3 {
      background: #f0f0f0;
      color: #2c3e50;
    }
  
   



    .logo-grid{
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  .hover-text span {
    max-height: 50%;
  margin-top: 25%;
  opacity: 0;
  transform: translateY(10px);
  display: inline-block;
  transition: opacity 0.3s ease, transform 0.3s ease;
  font-size: 1.4rem;
  font-family:system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  color: #89b8ca;
  font-weight: bold;
}


/* Default hidden state */
.logo-img:hover + .hover-text span {
  opacity: 1;
  transform: translateY(0);
}

.logo-img:hover + .hover-text span:nth-child(1) {
  transition-delay: 0s;
}
.logo-img:hover + .hover-text span:nth-child(2) {
  transition-delay: 0.1s;
}
.logo-img:hover + .hover-text span:nth-child(3) {
  transition-delay: 0.2s;
}

  .logo-img{
		max-width:5rem;
	}
    #logo{
       float: left;
       border: none;
       background: transparent;
       cursor: pointer;
    }

    .logo-grid-section {
  background-color: #0f1114;
  padding: 4rem 2rem;
  text-align: center;
}

.cert-grid {
  display: grid;
  padding: 4rem 2rem;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 2rem;
  align-items: center;
  justify-items: center;
  max-width: 800px;
  margin: 0 auto;
}

.cert {
  max-width: 100px;
  opacity: 0.85;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.cert:hover {
  transform: scale(1.05);
  opacity: 1;
}

    @font-face {
    font-family: 'Quicksand';
    font-style: normal;
    font-weight: 700;
    src: url('/fonts/QuicksandbookRegular-0gW4.otf') format('truetype'); /* IE9 Compat Modes */
    }

    .grid-item{
        padding: 3rem;
        text-align: center;
        font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
        color:#6b6c6c;
        background-color: #f2f2f2;
        border-radius: 15px;
    }

    .cert-item{
        padding: 1rem;
        text-align: center;
        font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
        color: #e6e6e6;
        border-radius: 40px;
        font-size: 1rem;
        background: linear-gradient(to bottom right, #6c96c6, #3f6f86);
    }

    .grid-item p {
        color: dimgray;
    }
    .grid{
        column-gap: 1rem;
        row-gap: 1rem;
        padding: 3rem;
        width: 70%;
        margin: auto;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        /* grid-template-rows: 1fr 1fr 1fr; */
        text-align: left;
    }

    .icon-title-grid{
        display: grid;
        grid-template-columns: 1fr 5fr;
    }

    .icon{
        max-width: 90%;
        margin-top: 1.5rem;
    }

    .email-txt{
        font-family:Inter, system-ui, Avenir, Helvetica, Arial, sans-serif; 
    }

    .contact-section {
    background-color: #0f1114;
    color: #e0e0e0;
    padding: 6rem 2rem;
    text-align: center;
  }

  .container {
    max-width: 700px;
    margin: 0 auto;
  }

  .section2-title{
    font-size: 2.5rem;
    color: #969a9d;
    padding-top:4rem;
  }

  .section3-title {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    color: #5b5b5b;
    font-family: "Quicksand";}

  .section3-text {
    font-size: 1.1rem;
    line-height: 1.6;
    margin-bottom: 2rem;
    color: #bbbbbb;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .email-link {
    display: inline-block;
    font-size: 1.1rem;
    font-weight: bold;
    color: #89b8ca;
    text-decoration: none;
    border-bottom: 2px solid transparent;
    transition: border-color 0.3s ease;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .email-link:hover {
    border-color: #89b8ca;
  }

     /* Responsive Styles */
     @media (max-width: 768px) {
      .nav-links {
        display: none;
      }
  
      .hamburger {
        display: block;
        color: #2c3e50;
      }
  
      .mobile-menu.show {
        display: flex;
      }

      .grid{
        grid-template-columns: 1fr;
        width: 90%;
        padding: 0;
      }
      .icon{
        width: 75%;
      }

      .section h1 {
        font-size: 2rem;
      }
    }
  </style>
  
  
  
  
