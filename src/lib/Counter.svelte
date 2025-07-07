<script>
  import { onMount } from 'svelte';
  import { spring } from 'svelte/motion';

  let countdown = {};
  let interval;

  const launchDate = new Date();
  launchDate.setDate(launchDate.getDate() + 30);

  const updateCountdown = () => {
    const now = new Date();
    const timeLeft = launchDate - now;

    if (timeLeft <= 0) {
      clearInterval(interval);
      countdown = { days: 0, hours: 0, minutes: 0, seconds: 0 };
      return;
    }

    countdown = {
      days: Math.floor(timeLeft / (1000 * 60 * 60 * 24)),
      hours: Math.floor((timeLeft / (1000 * 60 * 60)) % 24),
      minutes: Math.floor((timeLeft / 1000 / 60) % 60),
      seconds: Math.floor((timeLeft / 1000) % 60)
    };
  };

  onMount(() => {
    updateCountdown();
    interval = setInterval(updateCountdown, 1000);
  });
</script>

<style>
  body {
    margin: 0;
    font-family: 'Helvetica Neue', sans-serif;
    background: #fdfbff;
    color: #1c1c1c;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .container {
    text-align: center;
    max-width: 500px;
    padding: 2rem;
    background: white;
    border-radius: 1rem;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
  }

  h1 span {
    color: #ec008c;
  }

  h2 {
    margin: 0;
    color: #333;
  }

  .countdown {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin: 2rem 0;
  }

  .box {
    background: #f5f5f5;
    padding: 1rem;
    border-radius: 0.5rem;
    min-width: 60px;
  }

  .box strong {
    display: block;
    font-size: 1.5rem;
  }

  input {
    padding: 0.75rem;
    width: 100%;
    border-radius: 0.5rem;
    border: 1px solid #ccc;
    margin-bottom: 1rem;
  }

  button {
    padding: 0.75rem;
    width: 100%;
    background: linear-gradient(to right, #f000b8, #a933ff);
    color: white;
    border: none;
    border-radius: 0.5rem;
    font-weight: bold;
    cursor: pointer;
  }

  .note {
    font-size: 0.85rem;
    color: #777;
    margin-top: 1rem;
  }
</style>

<div class="container">
  <h1><span>SihriTen</span> demleniyor...</h1>
  <h2>Büyüleyici iç giyim yakında Türkiye'de.</h2>
  <p><strong>Listede kalın.</strong></p>

  <div class="countdown">
    <div class="box"><strong>{countdown.days}</strong><small>Gün</small></div>
    <div class="box"><strong>{countdown.hours}</strong><small>Saat</small></div>
    <div class="box"><strong>{countdown.minutes}</strong><small>Dakika</small></div>
    <div class="box"><strong>{countdown.seconds}</strong><small>Saniye</small></div>
  </div>

  <input type="email" placeholder="Email adresinizi girin" />
  <button>Bekleme Listesine Katıl</button>
  <p class="note">SihriTen'i ilk deneyimleyen siz olun.<br>Gizliliğinize saygı duyuyoruz. Spam yok—istediğiniz zaman abonelikten çıkabilirsiniz.</p>
</div>
