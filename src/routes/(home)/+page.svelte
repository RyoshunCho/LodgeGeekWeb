<script>
  import WALL7 from "$lib/img/manage/70.jpg";
  import WALL7_ALT from "$lib/img/manage/7.jpg";
  import WALL10 from "$lib/img/manage/10.jpg";
  import WALL11 from "$lib/img/manage/11.png";
  import WALL14 from "$lib/img/manage/14.jpg";
  import CheckAll from "svelte-material-icons/CheckAll.svelte";
  import MapMarkerRadius from "svelte-material-icons/MapMarkerRadius.svelte";
  import Cellphone from "svelte-material-icons/Cellphone.svelte";
  import EmailOutline from "svelte-material-icons/EmailOutline.svelte";
  import backgroundVideo from "$lib/video/boat.mp4";
  import MetaTagComponent from "../Components/MetaTagComponent.svelte";
  import Mountain1 from "$lib/img/category/mountain-1.jpg";
  import Mountain2 from "$lib/img/category/mountain-2.jpg";
  import Mountain3 from "$lib/img/category/mountain-3.jpg";
  import Mountain4 from "$lib/img/category/mountain-4.jpg";

  import { trans, locale } from "$lib/language/i18n";
  import { browser, building, dev, version } from "$app/environment";
  import { onMount } from 'svelte';
  import ContactForm from '../Components/ContactForm.svelte';
  import { useForm } from "svelte-use-form";

  const heroCards = [
    {
      image: Mountain1,
      titleKey: "hero.section.planning",
      href: "/management-service",
      btnHover: "navy"
    },
    {
      image: Mountain2,
      titleKey: "hero.section.consultant",
      href: "/consulting-service",
      btnHover: "seagreen"
    },
    {
      image: Mountain3,
      titleKey: "hero.section.iotSales",
      href: "/iot-service",
      btnHover: "palevioletred"
    },
    {
      image: Mountain4,
      titleKey: "photography_planning",
      href: "/homestay-photographing",
      btnHover: "rgb(81, 178, 235)"
    }
  ];

  let isContactVisible = false;
  let heroVideo;
  let isVideoMuted = false;

  if (browser) {
	  isContactVisible = window?.location?.hash === '#contact';
	}

	onMount(() => {
		isContactVisible = window.location.hash === '#contact';

		
	
		const handleHashChange = () => {
			isContactVisible = window.location.hash === '#contact';
			if (isContactVisible) {
			const contactSection = document.getElementById('contact');
			if (contactSection) {
				contactSection.scrollIntoView({ behavior: 'smooth' });
			}
			}
		};

		window.addEventListener('hashchange', handleHashChange);
		isContactVisible=true;
		return () => {
			window.removeEventListener('hashchange', handleHashChange);
		};
	});

  onMount(() => {
    if (!heroVideo) return;
    const playAttempt = heroVideo.play();
    if (playAttempt && typeof playAttempt.catch === "function") {
      playAttempt.catch(() => {
        isVideoMuted = true;
        heroVideo.muted = true;
        heroVideo.play().catch(() => {});
      });
    }
  });

  function toggleVideoAudio(event) {
    event.preventDefault();
    if (!heroVideo) return;
    if (isVideoMuted) {
      isVideoMuted = false;
      heroVideo.muted = false;
      heroVideo.play().catch(() => {});
      return;
    }
    isVideoMuted = true;
    heroVideo.muted = true;
  }

  if (browser) {
    // @ts-ignore
    let userLang = window.navigator.language || navigator.userLanguage;

    //   console.log(userLang);

    if (userLang === "ja") {
      $locale = "日本語";
    } else if (userLang === "zh-CN") {
      $locale = "中文";
    } else {
      $locale = "English";
    }
  }

  const inquireForm = useForm();
  let customerName = "",
    customerEmail = "",
    title = "",
    customerMessage = "";

  let status = "0";
  /**
   * @description お問い合わせフォームのバリデーション
   */

  console.log(import.meta.env.BASE_URL); // BASE_URLの値をコンソールに出力
</script>

<svelte:head>
  <MetaTagComponent />
  <link href="https://fonts.googleapis.com" rel="preconnect" />
  <link href="https://fonts.gstatic.com" rel="preconnect" />
  <link
    href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap"
    rel="stylesheet"
  />
  <link
    rel="stylesheet"
    href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css"
  />
</svelte:head>



<!-- Hero Section -->

<!-- /Hero Section -->


<section id="hero" class=" section module">
	<video bind:this={heroVideo} autoplay muted={isVideoMuted} playsinline loop class="hero-video">
		<source src={backgroundVideo} type="video/mp4" />
	  </video>
    <button class="hero-audio-toggle" type="button" on:click={toggleVideoAudio}>
      {isVideoMuted ? "Muted" : "Mute"}
    </button>

	<div class="hero-banner" aria-label="Hero services banner">
		<div class="hero-track">
      <div class="hero-group">
        {#each heroCards as card}
          <div class="hero-card card" style={`--btn-hover: ${card.btnHover};`}>
            <img src={card.image} class="card-img-top" alt={$trans(card.titleKey)} />
            <h5 class="card-title text-light">{$trans(card.titleKey)}</h5>
            <a href={card.href} class="btn btn-light">Link</a>
          </div>
        {/each}
      </div>
      <div class="hero-group" aria-hidden="true">
        {#each heroCards as card}
          <div class="hero-card card" style={`--btn-hover: ${card.btnHover};`}>
            <img src={card.image} class="card-img-top" alt={$trans(card.titleKey)} />
            <h5 class="card-title text-light">{$trans(card.titleKey)}</h5>
            <a href={card.href} class="btn btn-light" tabindex="-1">Link</a>
          </div>
        {/each}
      </div>
		</div>
	</div>
</section>

<!-- About Section -->
<section id="about" class="about section">
  <div class="container" data-aos="fade-up" data-aos-delay="100">
    <div class="row gy-4">
      <div class="col-lg-6 order-1 order-lg-2">
        <div class="about-image-rotator">
          <img src={WALL7} class="img-fluid" alt="LodgeGeek showcase image 1" />
          <img src={WALL7_ALT} class="img-fluid" alt="LodgeGeek showcase image 2" />
          <img src={WALL10} class="img-fluid" alt="LodgeGeek showcase image 3" />
          <img src={WALL11} class="img-fluid" alt="LodgeGeek showcase image 4" />
          <img src={WALL14} class="img-fluid" alt="LodgeGeek showcase image 5" />
        </div>
      </div>
      <div class="col-lg-6 order-2 order-lg-1 content">
        <h3>About Us</h3>
        <p class="mb-3">
          {$trans("about.section.title")}
        </p>
        <ul>
          <li>
            <div style="margin-right:0.5rem;">
              <CheckAll color="#ffc451" width="32" height="32" />
            </div>
            <span>{$trans("about.section.vision1")}</span>
          </li>
          <li>
            <div style="margin-right:0.5rem;">
              <CheckAll color="#ffc451" width="32" height="32" />
            </div>
            <span>{$trans("about.section.vision2")}</span>
          </li>
          <li>
            <div style="margin-right:0.5rem;">
              <CheckAll color="#ffc451" width="32" height="32" />
            </div>
            <span>{$trans("about.section.vision3")}</span>
          </li>
        </ul>
        <p>
          {$trans("about.section.vision.end")}
        </p>
      </div>
    </div>
  </div>
</section>
<!-- /About Section -->



<!-- Contact Section -->
<section id="contact" class="contact section">
  <!-- Section Title -->
  <div class="container section-title" data-aos="fade-up">
    <h2>Contact</h2>
    <p>Contact Us</p>
  </div>
  <!-- End Section Title -->

  <div class="container" data-aos="fade-up" data-aos-delay="100">
    <div class="mb-5">
      <iframe
        style="border:0; width: 100%; height: 270px;"
        src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d6482.7408347996625!2d139.8547251!3d35.6678802!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x601888756278020d%3A0x58adabc057d1728b!2z44CSMTM0LTAwODgg5p2x5Lqs6YO95rGf5oi45bed5Yy66KW_6JGb6KW_77yS5LiB55uu77yS77yS4oiS77yU77yV!5e0!3m2!1sja!2sjp!4v1717805375116!5m2!1sja!2sjp"
        frameborder="0"
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
		title="Google Maps"
      ></iframe>
    </div>
    <!-- End Google Maps -->

    <div class="row gy-4">
      <div class="col-lg-4">
        <div class="info-item d-flex" data-aos="fade-up" data-aos-delay="300">
          <div class="icon">
            <MapMarkerRadius color="#ffc451" width="36" height="36" />
          </div>

          <div>
            <h3>Address</h3>
            <p>〒134-0088 東京都江戸川区西葛西2-22-45 542室</p>
            <p>
              Room.542, 2-22-45, Nishikasai, Edogawaku, Tokyo, 134-0088, Japan
            </p>
          </div>
        </div>
        <!-- End Info Item -->

        <div class="info-item d-flex" data-aos="fade-up" data-aos-delay="400">
          <div class="icon">
            <Cellphone color="#ffc451" width="36" height="36" />
          </div>
          <div>
            <h3>Call Us</h3>
            <p><a href="tel:03-6824-7905">Japan Local: 03-6824-7905</a></p>
            <p><a href="tel:+81368247905">International: +81-368247905</a></p>
          </div>
        </div>
        <!-- End Info Item -->

        <div class="info-item d-flex" data-aos="fade-up" data-aos-delay="500">
          <div class="icon">
            <EmailOutline color="#ffc451" width="36" height="36" />
          </div>
          <div>
            <h3>Email Us</h3>
            <p>
              <a href="mailTo:contact@lodgegeek.com" class="__cf_email__"
                >contact@lodgegeek.com
              </a>
            </p>
          </div>
        </div>
      </div>

      <!-- Start of Contact Form (Tallyを使用)-->
      <div class="col-lg-8">
        <!-- <div class="wrap">
          <iframe
            data-tally-src="https://tally.so/embed/meBRqQ?alignLeft=1&hideTitle=1&transparentBackground=1&dynamicHeight=1"
            loading="lazy"
            width="100%"
            height="313"
            frameborder="0"
            marginheight="0"
            marginwidth="0"
			referrerpolicy="no-referrer-when-downgrade"
            title="Contact Form"
          ></iframe>
		  <script>
            var d = document,
              w = "https://tally.so/widgets/embed.js",
              v = function () {
                "undefined" != typeof Tally
                  ? Tally.loadEmbeds()
                  : d
                      .querySelectorAll("iframe[data-tally-src]:not([src])")
                      .forEach(function (e) {
                        e.src = e.dataset.tallySrc;
                      });
              };
            if ("undefined" != typeof Tally) v();
            else if (d.querySelector('script[src="' + w + '"]') == null) {
              var s = d.createElement("script");
              (s.src = w),
                (s.onload = v),
                (s.onerror = v),
                d.body.appendChild(s);
            }
          </script>
        </div> -->
		<ContactForm visible={isContactVisible} />
	  </div>
      <!-- End of Contact Form (Tallyを使用)-->

      <!-- Start Contact Form 
			<div class="col-lg-8">
			  <form class="php-email-form"  use:inquireForm>
				<div class="row gy-4" style="{status=="1" || status=="2" ? "display:none" : ""}">
				  <div class="col-md-6">
					<input type="text" name="name" class="form-control" placeholder="Your Name" 
					 bind:value={customerName} 
					 use:validators={[required,minLength(2)]}
					 >
					 <div class="use-form-hint">
						<HintGroup for="name">
						  <Hint on="required">名前を入力ください。</Hint>
						  <Hint on="minLength">2文字を入力ください。</Hint>
						</HintGroup>
					  </div>					 
				  </div>
  
				  <div class="col-md-6 ">
					<input type="email" class="form-control" name="email" placeholder="Your Email" bind:value={customerEmail} use:validators={[required,email]} >
					<div class="use-form-hint">
						<HintGroup for="email">
						  <Hint on="required">Emailを入力ください。</Hint>
						  <Hint on="email">Emailが不正です。</Hint>
						</HintGroup>
					</div>
				  </div>
  
				  <div class="col-md-12">
					<input type="text" class="form-control" name="subject" placeholder="Subject" bind:value={title} use:validators={[required,minLength(4),maxLength(50)]} >
					<div class="use-form-hint">
						<HintGroup for="subject">
						  <Hint on="required">subjectを入力ください。</Hint>
						  <Hint on="minLength">4文字以上を入力ください。</Hint>
						  <Hint on="maxLength">50文字以下を入力ください。</Hint>
						</HintGroup>
					</div>
				  </div>
  
				  <div class="col-md-12">
					<textarea class="form-control" name="message" rows="6" placeholder="Message" bind:value={customerMessage} use:validators={[required,minLength(4),maxLength(200)]}></textarea>
					<div class="use-form-hint">
						<HintGroup for="message">
						  <Hint on="required">messageを入力ください。</Hint>
						  <Hint on="minLength">4文字以上を入力ください。</Hint>
						  <Hint on="maxLength">200文字以下を入力ください。</Hint>
						</HintGroup>
					</div>
				  </div>
				</div>

				<div class="col-md-12 text-center">
					<div class="loading" style="{status=="1" ? "display:block" : ""}">Loading</div>
					<div class="sent-message" style="{status=="2" ? "display:block" : ""}">Your message has been sent. Thank you!</div>
				  </div>				
			  </form>
			  <div class="col-md-12 text-center" style="{status=="2" ? "display:none" : ""}">
					<button class="submit" disabled={!$inquireForm.valid } on:click={()=>{inquireAction()}}>Send Message</button>
			  </div>			  
			</div>
			End of Contact Form -->
    </div>
  </div>
</section>

<!-- /Contact Section -->

<style>
  @keyframes square-in-center {
    from {
      clip-path: inset(100% 100% 100% 100%);
    }
    to {
      clip-path: inset(0 0 0 0);
    }
  }

  .hero-video {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .hero-audio-toggle {
    position: fixed;
    top: 84px;
    right: 20px;
    z-index: 1100;
    padding: 4px 10px;
    border-radius: 999px;
    border: 1px solid rgba(255, 255, 255, 0.6);
    background: rgba(17, 17, 17, 0.75);
    color: #fff;
    font-size: 11px;
    letter-spacing: 0.02em;
    cursor: pointer;
    transition: background 0.2s ease, transform 0.2s ease, border-color 0.2s ease;
    animation: hero-audio-pulse 2.2s ease-in-out infinite;
  }

  .hero-audio-toggle:hover {
    background: rgba(17, 17, 17, 0.9);
    border-color: rgba(255, 255, 255, 0.9);
    transform: translateY(-1px);
  }

  .hero-audio-toggle:focus-visible {
    outline: 2px solid #ffc451;
    outline-offset: 2px;
  }

  @keyframes hero-audio-pulse {
    0%, 100% {
      box-shadow: 0 0 0 0 rgba(255, 255, 255, 0.25);
    }
    50% {
      box-shadow: 0 0 0 8px rgba(255, 255, 255, 0.0);
    }
  }

  @media (max-width: 768px) {
    .hero-audio-toggle {
      top: 76px;
      right: 16px;
    }
  }

  .module, .module-small {
    position: relative;
    padding: 140px 0;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-size: cover;
}



@-webkit-keyframes animation-bg {
0% {
  background-position: 50% 100%;
}
100% {
  background-position: 50% 0%;
}
}
@keyframes animation-bg {
0% {
  background-position: 50% 100%;
}
100% {
  background-position: 50% 0%;
}
}

section
{
  margin-top:5rem;
}

#hero {
  --hero-video-height: clamp(680px, 90vh, 980px);
  --hero-banner-shift: 23px;
  --hero-banner-space: 0px;
  position: relative;
  padding: 0 0 var(--hero-banner-space);
  margin-top: 0;
  height: var(--hero-video-height);
  overflow: visible;
}

.about-image-rotator {
  display: grid;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 18px 40px rgba(0, 0, 0, 0.18);
  aspect-ratio: 4 / 3;
}

.about-image-rotator img {
  grid-area: 1 / 1;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0;
  animation: about-rotate 17.5s infinite;
  transition: transform 0.4s ease;
  will-change: transform, opacity;
}

.about-image-rotator img:nth-child(1) {
  animation-delay: 0s;
}

.about-image-rotator img:nth-child(2) {
  animation-delay: 3.5s;
}

.about-image-rotator img:nth-child(3) {
  animation-delay: 7s;
}

.about-image-rotator img:nth-child(4) {
  animation-delay: 10.5s;
}

.about-image-rotator img:nth-child(5) {
  animation-delay: 14s;
}

.about-image-rotator:hover img {
  transform: scale(1.03);
}

@keyframes about-rotate {
  0% {
    opacity: 0;
  }
  2.86% {
    opacity: 1;
  }
  20% {
    opacity: 1;
  }
  22.86% {
    opacity: 0;
  }
  100% {
    opacity: 0;
  }
}

.hero-banner {
  position: absolute;
  z-index: 1;
  left: 0;
  right: 0;
  bottom: 0;
  margin-top: 0;
  transform: translateY(var(--hero-banner-shift));
  overflow-x: hidden;
  overflow-y: visible;
  width: 100%;
  padding: 0 2rem 48px;
}

.hero-track {
  display: flex;
  align-items: center;
  width: max-content;
  animation: hero-marquee 72s linear infinite;
}

.hero-group {
  display: flex;
  align-items: center;
  gap: 2rem;
  padding-right: 2rem;
  flex-shrink: 0;
}

.hero-banner:hover .hero-track {
  animation-play-state: paused;
}

@keyframes hero-marquee {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-50%);
  }
}

.hero-card
{
  -webkit-transition: all .2s ease-out;
-moz-transition: all .2s ease-out;
-ms-transition: all .2s ease-out;
-o-transition: all .2s ease-out;
 transition: all .2s ease-out;
border-radius:15px;
border:none;
  background-color:white;
  flex: 0 0 auto;
  width: clamp(156px, 18.2vw, 273px);
  height: clamp(104px, 13vw, 156px);
  position: relative;
  margin: 0;
  overflow: visible;
}


.hero-card .btn 
{
opacity:0;  
position:absolute;
left:50%;
bottom: 0;
transform: translate(-50%, 50%);
 box-shadow: 0 4px 18px 0 rgba(0, 0, 0, 0);
-webkit-transition: all .2s ease-out;
-moz-transition: all .2s ease-out;
-ms-transition: all .2s ease-out;
-o-transition: all .2s ease-out;
 transition: all .2s ease-out;
border-radius: 10px;
padding:0.8rem 1.7rem;
border:none;
font-weight:bold;
z-index: 5;
}

.hero-card:hover .btn
{
opacity:1;
bottom: 0;
 box-shadow: 0 4px 18px 0 rgba(0, 0, 0, 0.25);
}

.hero-card:hover
{
box-shadow: 0 4px 18px 0 rgba(0,0,0,0.7);

}

.hero-card h5{
	position: absolute;
	left:50%;
	top: 50%;
	transform: translate(-50%, -50%);
	font-size: 1rem;
	opacity:0.8;
	text-shadow: 1px 1px 2px black;
	-webkit-transition: all .2s ease-out;
	-moz-transition: all .2s ease-out;
	-ms-transition: all .2s ease-out;
	-o-transition: all .2s ease-out;
	transition: all .2s ease-out;
  font-family: var(--default-font);
}

.hero-card:hover h5{
	opacity:1;
  font-size: 1.5rem;
}

.hero-card .btn:hover 
{
	color:white;
	border:none;
  background-color: var(--btn-hover);
}

.hero-card img
{
filter:blur(0px);
  -webkit-transition: all .2s ease-out;
-moz-transition: all .2s ease-out;
-ms-transition: all .2s ease-out;
-o-transition: all .2s ease-out;
 transition: all .2s ease-out;
border-radius:15px;
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.hero-card:hover img{
	filter:blur(3px);
}


  /* スマホ */
  @media only screen and (max-width: 767px) {
    .hero-video {
      margin-top: 0px;
      top: 0;
      transform: none;
    }


	.module, .module-small {
		padding: 40px 0;
	}
  }

  @media only screen and (min-width: 768px) {
    .hero-video {
      bottom: 0;
      width: 100%;
      margin-top: 0;
    }
  }
</style>
