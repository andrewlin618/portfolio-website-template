<script>
  import { onMount } from 'svelte';
  let darkMode = JSON.parse(localStorage.getItem('darkMode')) || false;
  let isNavExpended = false;
  let navWidth;
  let navHeight;

  let works = [
    { name: 'project 1', introduction: 'xxxxxxxxx' },
    { name: 'project 2', introduction: 'xxxxxxxxx' },
    { name: 'project 3', introduction: 'xxxxxxxxx' },
    { name: 'project 4', introduction: 'xxxxxxxxx' },
  ];
  let experiences = [
    { name: 'title 1', company: 'company1', time: 'xx/20XX - xx/20xx' },
    { name: 'title 2', company: 'company2', time: 'xx/20xx - xx/20xx' },
    { name: 'title 3', company: 'company3', time: 'xx/xxxx - xx/xxxx' },
    { name: 'title 4', company: 'company4', time: 'xx/xxxx - xx/xxxx' },
  ];
  const toggleDarkMode = () => {
    darkMode = !darkMode;
    localStorage.setItem('darkMode', darkMode ? 'true' : 'false');
    if (darkMode) {
      window.document.body.classList.add('dark-mode');
    } else {
      window.document.body.classList.remove('dark-mode');
    }
  };
  $: colors = darkMode
    ? {
        primary: 'blue',
        nav: '#111',
        about: '#333',
      }
    : {
        primary: 'salmon',
        nav: '#ddd',
        about: '#ccc',
      };

  onMount(() => {
    if (darkMode) {
      window.document.body.classList.add('dark-mode');
    }
  });
</script>

<main>
  <!-- Navbar "-->
  <nav style="background:{colors.nav}" bind:clientHeight={navHeight}>
    <section id="nav" bind:clientWidth={navWidth} style="--navHeight:{navHeight}">
      <div class="logo">
        <img src="./logo.svg" alt="logo" />
        <a href="/#">Xxx's website </a><br />
      </div>
      {#if navWidth >= 600}
        <a href="#about">About</a>
        <a href="#works">Work</a>
        <a href="#experiences">Experience</a>
        <a href="#contact">Contact</a>
      {:else}
        <button on:click={() => (isNavExpended = !isNavExpended)}>🍔</button>
      {/if}
      <button on:click={toggleDarkMode} style="width: 3rem; background: {colors.primary}; transition: 1s">
        <span style="position: relative; left: {darkMode ? '0.5rem' : '-0.5rem'}; transition:1s">
          {darkMode ? '🌛' : '🌞'}
        </span>
      </button>
    </section>
    {#if navWidth < 600 && isNavExpended}
      <ul style="padding-left:0; text-align: center">
        <a href="#about" on:click={() => (isNavExpended = false)}>About</a><br />
        <a href="#works" on:click={() => (isNavExpended = false)}>Work</a><br />
        <a href="#experiences" on:click={() => (isNavExpended = false)}>Experience</a><br />
        <a href="#contact" on:click={() => (isNavExpended = false)}>Contact</a>
      </ul>
    {/if}
  </nav>

  <!-- Home section -->
  <div>
    <section id="home">
      <div id="introduction">
        <h1>I am a Software Engineer</h1>
        <h3>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quasi odio optio, culpa sit commodi vero sapiente a.</h3>
      </div>
      <div id="profile-image">
        <img src="./profile.png" alt="" />
      </div>
    </section>
  </div>

  <!-- About section -->
  <div style="background: {colors.about};">
    <section id="about">
      <h2>About me</h2>
      <h3>
        Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quasi odio optio, culpa sit commodi vero sapiente a. Lorem ipsum dolor sit amet
        consectetur adipisicing elit. Numquam pariatur dicta fugit beatae, inventore rem exercitationem. Sapiente, cum sed possimus, unde nobis
        architecto numquam quod rerum exercitationem, dolorem ipsum. <br /><br />Hic!Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quasi
        odio optio, culpa sit commodi vero sapiente a. Lorem ipsum dolor sit amet consectetur adipisicing elit. Numquam pariatur dicta fugit beatae,
        inventore rem exercitationem. Sapiente, cum sed possimus, unde nobis architecto numquam quod rerum exercitationem, dolorem ipsum. <br /><br />
        Hic!Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quasi odio optio, culpa sit commodi vero sapiente a. Lorem ipsum dolor sit amet consectetur
        adipisicing elit. Numquam pariatur dicta fugit beatae, inventore rem exercitationem. Sapiente, cum sed possimus, unde nobis architecto numquam
        quod rerum exercitationem, dolorem ipsum.
      </h3>
    </section>
  </div>

  <!-- Work section -->
  <div>
    <section id="works">
      <h2>Work</h2>
      <div class="works">
        {#each works as work}
          <div class="work">
            <img src="./placeholder.png" alt="" /><br />
            <span>{work.name}</span>
          </div>
        {/each}
      </div>
    </section>
  </div>

  <!-- Experience section -->
  <div style="background: {darkMode ? '#333' : '#ccc'};">
    <section id="experiences">
      <h2>Experiences</h2>
      {#each experiences as e}
        <h3>{e.name} | {e.company} | {e.time}</h3>
        <hr />
        <li>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Numquam pariatur dicta fugit beatae, inventore rem exercitationem. Sapiente, cum
          sed possimus, unde nobis architecto numquam quod rerum exercitationem, dolorem ipsum. Hic!
        </li>
      {/each}
    </section>
  </div>

  <!-- Contact section -->
  <div>
    <section id="contact">
      <h2>Contact</h2>
      <form>
        <label for="name"> Name: </label><br />
        <input id="name" type="text" /><br />
        <label for="email">Email:</label><br />
        <input id="email" type="text" /><br />
        <label for="message">Message:</label><br />
        <textarea id="message" rows="10" style="resize: none;" />
        <div style="display:flex; justify-content:end">
          <button on:click|preventDefault={() => alert('Feature not implemented yet!')} style="background:{colors.primary}">Submit</button>
        </div>
      </form>
      <div class="social">
        <button>linkedin</button>
        <button>github</button>
        <button>ins</button>
      </div>
    </section>
  </div>
</main>

<style>
  main {
    width: 100%;
    min-height: 100vh;
  }

  section {
    max-width: 1400px;
    margin: auto;
    padding: 1rem;
    scroll-margin-top: 4rem;
  }

  /* nav style */
  nav {
    position: fixed;
    width: calc(100% - 16px);
    top: 0px;
  }

  #nav {
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-right: auto;
  }

  .logo img {
    width: 2rem;
  }

  /* sections style */
  #home {
    min-height: 600px;
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    flex-wrap: wrap;
  }

  #introduction {
    max-width: 700px;
    padding: 1rem;
  }

  #profile-image {
    max-width: 300px;
    max-height: 300px;
  }

  img {
    width: 100%;
  }

  #about {
    padding: 2rem;
  }

  .works {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 2rem;
  }

  .work {
    width: clamp(300px, 50%, 580px);
    text-align: center;
  }

  .work img {
    width: 100%;
  }

  #experiences {
    padding: 2rem;
    max-width: 1000px;
    margin: auto;
  }

  #contact {
    min-height: 94vh;
  }

  form {
    max-width: 800px;
    margin: auto;
  }

  #contact input {
    padding: 0.5rem;
  }

  #contact textarea {
    padding: 0.5rem;
    width: 100%;
  }

  .social {
    display: flex;
    justify-content: center;
    margin-top: 2rem;
    gap: 1rem;
  }

  button {
    padding: 0.3rem;
    border: 1px solid;
    border-radius: 2rem;
    color: inherit;
  }

  h2 {
    text-align: center;
  }

  h3 {
    margin-bottom: 0;
  }
</style>
