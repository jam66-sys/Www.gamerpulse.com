<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Game Pulse — Top Gaming Hub</title>
<style>
  * {
    box-sizing: border-box;
    margin: 0; padding: 0;
  }
  body, html {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #0a0a0f;
    color: #cbd5e1;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  header {
    background: linear-gradient(90deg, #7f00ff, #e100ff);
    color: #f0f0f0;
    padding: 18px 20px;
    font-size: 2rem;
    font-weight: 900;
    text-align: center;
    user-select: none;
    box-shadow: 0 3px 15px #7f00ffaa;
  }
  nav {
    background: #11111a;
    display: flex;
    justify-content: center;
    gap: 18px;
    padding: 14px 10px;
  }
  nav button {
    background: #7f00ff;
    border: none;
    padding: 12px 28px;
    border-radius: 12px;
    color: #fff;
    font-weight: 700;
    cursor: pointer;
    font-size: 1rem;
    transition: background 0.3s ease;
    user-select: none;
  }
  nav button:hover,
  nav button.active {
    background: #b14eff;
    box-shadow: 0 0 8px #b14effaa;
  }
  main {
    flex-grow: 1;
    overflow-y: auto;
    background: #1a1a2e;
    padding: 24px 20px;
  }
  section {
    display: none;
    max-width: 900px;
    margin: 0 auto;
  }
  section.active {
    display: block;
  }
  .game-post {
    background: #22223b;
    margin-bottom: 28px;
    border-radius: 16px;
    box-shadow: 0 0 12px #b14effaa;
    overflow: hidden;
    cursor: default;
    user-select: none;
  }
  .game-post:hover {
    box-shadow: 0 0 20px #e100ffdd;
  }
  .game-banner {
    width: 100%;
    height: 220px;
    object-fit: cover;
  }
  .game-info {
    padding: 18px 22px;
  }
  .game-title {
    font-size: 1.6rem;
    font-weight: 900;
    color: #e100ff;
    margin-bottom: 8px;
  }
  .game-description {
    font-size: 1.1rem;
    line-height: 1.4;
    color: #cbd5e1dd;
  }
  #loginPage {
    background: #22223b;
    padding: 32px 28px;
    border-radius: 16px;
    box-shadow: 0 0 14px #7f00ffaa;
    max-width: 360px;
    margin: 36px auto;
    text-align: center;
    user-select: none;
  }
  #loginPage h2 {
    margin-bottom: 28px;
    color: #e100ff;
    font-weight: 900;
    font-size: 1.8rem;
  }
  #loginForm input {
    width: 100%;
    padding: 14px 18px;
    margin-bottom: 20px;
    border-radius: 14px;
    border: none;
    font-size: 1rem;
    outline: none;
  }
  #loginForm input:focus {
    box-shadow: 0 0 12px #b14effdd;
  }
  #loginForm button {
    width: 100%;
    padding: 14px 0;
    border-radius: 16px;
    border: none;
    background: #7f00ff;
    color: #fff;
    font-weight: 900;
    font-size: 1.2rem;
    cursor: pointer;
    user-select: none;
    transition: background 0.3s ease;
  }
  #loginForm button:hover {
    background: #b14eff;
  }
  #googleLoginBtn {
    margin-top: 18px;
    background: #4285f4;
  }
  #googleLoginBtn:hover {
    background: #357ae8;
  }
  #userInfo {
    margin-top: 22px;
    font-weight: 700;
    color: #b14eff;
  }
  @media (max-width: 480px) {
    .game-banner {
      height: 140px;
    }
    header {
      font-size: 1.4rem;
      padding: 12px 10px;
    }
    nav {
      padding: 12px 5px;
      gap: 12px;
    }
    nav button {
      padding: 10px 14px;
      font-size: 0.9rem;
    }
    main {
      padding: 18px 12px;
    }
    #loginPage {
      margin: 24px 12px;
      padding: 24px 16px;
    }
  }
</style>
</head>
<body>

<header>Game Pulse — Top Gaming Hub</header>

<nav>
  <button id="navFeed" class="active">Top Games</button>
  <button id="navLogin">Sign In</button>
</nav>

<main>
  <!-- Feed Section -->
  <section id="feed" class="active">

    <!-- 20 games feed -->
    <!-- (Same as your posted game posts) -->
    <!-- Fortnite -->
    <article class="game-post">
      <img class="game-banner" src="https://cdn2.unrealengine.com/fortnite-home-1920x1080-1920x1080-10d2fdb5c20a.jpg" alt="Fortnite" />
      <div class="game-info">
        <h3 class="game-title">Fortnite</h3>
        <p class="game-description">The massively popular battle royale with vibrant graphics, building mechanics, and endless events.</p>
      </div>
    </article>
    <!-- Add other game posts here (copy your 20 games as you wrote them) -->

    <!-- For brevity here: just copy your existing 20 articles in the final file -->
  </section>

  <!-- Login Section -->
  <section id="loginPage" style="display:none;">
    <form id="loginForm">
      <h2>Sign In to Game Pulse</h2>
      <input type="email" id="email" placeholder="Email" autocomplete="username" required />
      <input type="password" id="password" placeholder="Password" autocomplete="current-password" required />
      <button type="submit">Login</button>
      <button type="button" id="googleLoginBtn">Sign in with Google</button>
    </form>
    <div id="userInfo">Not signed in</div>
  </section>
</main>

<script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-auth.js"></script>
<script>
  // Your Firebase config — replace with your actual config from Firebase Console!
  const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
  };

  firebase.initializeApp(firebaseConfig);
  const auth = firebase.auth();

  // DOM Elements
  const navFeed = document.getElementById('navFeed');
  const navLogin = document.getElementById('navLogin');
  const feed = document.getElementById('feed');
  const loginPage = document.getElementById('loginPage');
  const loginForm = document.getElementById('loginForm');
  const emailInput = document.getElementById('email');
  const passwordInput = document.getElementById('password');
  const userInfo = document.getElementById('userInfo');
  const googleLoginBtn = document.getElementById('googleLoginBtn');

  // Show/hide sections
  function showSection(section) {
    feed.style.display = 'none';
    loginPage.style.display = 'none';
    section.style.display = 'block';
  }
  function setActive(button) {
    navFeed.classList.remove('active');
    navLogin.classList.remove('active');
    button.classList.add('active');
  }

  navFeed.onclick = () => {
    showSection(feed);
    setActive(navFeed);
  };
  navLogin.onclick = () => {
    showSection(loginPage);
    setActive(navLogin);
  };

  // Initialize view
  showSection(feed);

  // Login form submit
  loginForm.onsubmit = e => {
    e.preventDefault();
    const email = emailInput.value.trim();
    const password = passwordInput.value;
    auth.signInWithEmailAndPassword(email, password)
      .then(({ user }) => {
        userInfo.textContent = `Signed in as: ${user.email}`;
        loginForm.reset();
        showSection(feed);
        setActive(navFeed);
      })
      .catch(err => alert("Login error: " + err.message));
  };

  // Google sign-in
  googleLoginBtn.onclick = () => {
    const provider = new firebase.auth.GoogleAuthProvider();
    auth.signInWithPopup(provider)
      .then(({ user }) => {
        userInfo.textContent = `Signed in as: ${user.displayName || user.email}`;
        showSection(feed);
        setActive(navFeed);
      })
      .catch(err => alert("Google login error: " + err.message));
  };

  // Firebase auth state listener
  auth.onAuthStateChanged(user => {
    if (user) {
      userInfo.textContent = `Signed in as: ${user.displayName || user.email}`;
      showSection(feed);
      setActive(navFeed);
    } else {
      userInfo.textContent = "Not signed in";
      showSection(feed);
      setActive(navFeed);
    }
  });
</script>

</body>
</html>
