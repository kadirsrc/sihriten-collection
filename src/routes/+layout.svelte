<script>
  import { webVitals } from '$lib/vitals';
  import { browser } from '$app/env';
  import { page } from '$app/stores';
  import '../app.css';

  let analyticsId = import.meta.env.VERCEL_ANALYTICS_ID;

  $: if (browser && analyticsId) {
    webVitals({
      path: $page.url.pathname,
      params: $page.params,
      analyticsId
    })
  }
</script>


<main>
	<slot />
</main>

<footer>
	<p class="note">Gizliliğinize saygı duyuyoruz. Spam yok—istediğiniz zaman abonelikten çıkabilirsiniz.</p>
</footer>

<style>
	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 1024px;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 40px;
	}

	footer a {
		font-weight: bold;
	}

	footer .note {
    font-size: 0.85rem;
    color: #777;
    margin-top: 1rem;
  	}

	@media (min-width: 480px) {
		footer {
			padding: 40px 0;
		}
	}
</style>
