<script>
    import Instagram from "svelte-material-icons/Instagram.svelte"
    import Whatsapp from "svelte-material-icons/Whatsapp.svelte"
    import Tooltip from "sv-tooltip"

    import { trans,locale, locales } from "$lib/language/i18n";
    import WECHAT from "$lib/img/socail/apps-wechat.svg";
    import LINE from "$lib/img/socail/icons8-line-96.png";
    import REDNOTE from "$lib/img/socail/rednote.png";
    import REDNOTEQR from "$lib/img/socail/reenoteQR.jpg";
    import WECHATQR from "$lib/img/socail/wechatQR.jpg";


</script>
<svelte:head>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</svelte:head>

<footer id="footer" class="footer">
    <div class="footer-top">
      <div class="container">
        <div class="row gy-4">
          <div class="col-lg-4 col-md-6 footer-about">
            <a href="/" class="logo d-flex align-items-center">
              <!--
              <span class="sitename">株式会社LodgeGeek</span>
              -->
              <span class="sitename">{$trans("footer.section.companyName")}</span>

            </a>
            
            <div class="footer-contact pt-3" >
              <p class="sitename custom-number">住宅宿泊管理業者
                <br>登録番号：国土交通大臣(01)第F037122号</p>
            </div>

            <div class="footer-contact pt-3">
              <p>{$trans("footer.section.address1")}
              </p>
              <p>{$trans("footer.section.address2")}</p>
              <p><strong>Phone(Japan Local):</strong> <span><a href="tel:03-6824-7905">03-6824-7905</a></span></p>
              <p><strong>Phone(International):</strong> <span><a href="tel:+81368247905">+81-368247905</a></span></p>
              <p><strong>Fax(Japan Local):</strong> <span> 03-4530-8790</span></p>
              <p><strong>Email:</strong> <span><a href="mailTo:contact@lodgegeek.com" class="__cf_email__" >contact@lodgegeek.com</a></span></p>
              <p><strong>WeChat:</strong> <span><a href="weixin://dl/chat?dinzzz" target="_blank" class="__cf_email__" >dinzzz</a></span></p>
              <p><strong>Line:</strong> <span><a href="https://line.me/R/ti/p/@834rjqcs" target="_blank" class="__cf_email__" >Line友だち追加</a></span></p>

            </div>
            <div class="social-links d-flex mt-4">
              <a href="https://line.me/R/ti/p/@834rjqcs" target="_blank"><img src="{LINE}" style="width: 36px;height:36px" alt="" /></a>
              <div class="qr-tooltip-container">
                <!-- svelte-ignore a11y-invalid-attribute -->
                <a href="javascript:void(0)" class="social-link">
                  <img src="{REDNOTE}" style="width: 36px;height:36px" alt="RedNote" />
                </a>
                <div class="qr-tooltip">
                  <div class="qr-tooltip-arrow"></div>
                  <img src="{REDNOTEQR}" alt="RedNote QR Code" class="qr-code-img"/>
                </div>
              </div>
              <div class="qr-tooltip-container">
                <!-- svelte-ignore a11y-invalid-attribute -->
                <a href="javascript:void(0)" class="social-link">
                  <img src="{WECHAT}" style="width: 36px;height:36px" alt="" />
                </a>
                <div class="qr-tooltip">
                  <div class="qr-tooltip-arrow"></div>
                  <img src="{WECHATQR}" alt="Wechat QR Code" class="qr-code-img"/>
                </div>
              </div>
              <a href="https://www.instagram.com/qiqi_house_tokyo?igsh=cWhndmljaHp3cmcy" target="_blank" rel="noreferrer">
                <Instagram color="white" width=36 height=36/>
              </a>
              <a href="https://wa.link/nydnxe" target="_blank"><Whatsapp color="white" width=36 height=36/></a>
              <!-- <Tooltip tip="WechatId:<br/>dinzzz<br/>" top color="coral">
                <a href="javascript:void(0)"><img src="{WECHAT}" style="width: 36px;height:36px" alt="" /></a>
              </Tooltip> -->

            </div>
          </div>

          <div class="col-lg-2 col-md-3 footer-links">
            <h4>Link</h4>
            <ul>
              <li><span class="material-icons">chevron_right</span> <a href="/#"> {$trans("memu.title.home")}</a></li>
              <li><span class="material-icons">chevron_right</span> <a href="/#about"> {$trans("memu.title.about")}</a></li>
              <li><span class="material-icons">chevron_right</span> <a href="/#hero"> {$trans("memu.title.service")}</a></li>
              <!-- <li><span class="material-icons">chevron_right</span> <a href="#"> Terms of service</a></li> -->
              <li><span class="material-icons">chevron_right</span> <a href="/term" target="_blank"> {$trans("footer.section.privacyPolicy")}   </a></li>
            </ul>
          </div>

          <div class="col-lg-2 col-md-3 footer-links">
            <h4>Our Services</h4>
            <ul>
              <li><span class="material-icons">chevron_right</span> <a href="/management-service"> {$trans("services.section.job1")}</a></li>
              <li><span class="material-icons">chevron_right</span> <a href="/iot-service"> {$trans("services.section.job2")}</a></li>
              <li><span class="material-icons">chevron_right</span> <a href="/consulting-service"> {$trans("services.section.job3")}</a></li>
              <li><span class="material-icons">chevron_right</span> <a href="/homestay-photographing"> {$trans("photography_planning")}</a></li>
            </ul>
          </div>


        </div>
      </div>
    </div>

    <div class="copyright">
      <div class="container text-center">
        <p>© <span>Copyright</span> <strong class="px-1 sitename">LodgeGeek Co., Ltd.</strong> <span>All Rights Reserved</span></p>
        <div class="credits">
          Designed by <a href="/">LodgeGeek Co., Ltd.</a> with ❤️️
        </div>
      </div>
    </div>

</footer>

<style>
  .qr-tooltip-container {
    position: relative;
    display: inline-block;
  }

  .social-link {
    display: flex;
    justify-content: center;
    align-items: center;
    transition: transform 0.2s ease;
  }

  .social-link:hover {
    transform: translateY(-2px);
  }

  .qr-tooltip {
    position: absolute;
    bottom: 100%;
    left: 50%;
    transform: translateX(-50%);
    margin-bottom: 15px;
    padding: 10px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.15);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
    z-index: 1000;
  }

  .qr-tooltip-arrow {
    position: absolute;
    bottom: -8px;
    left: 50%;
    transform: translateX(-50%);
    width: 0;
    height: 0;
    border-left: 8px solid transparent;
    border-right: 8px solid transparent;
    border-top: 8px solid white;
  }

  .qr-code-img {
    width: 300px;
    height: 300px;
    display: block;
    border-radius: 4px;
  }

  /* Show tooltip on hover */
  .qr-tooltip-container:hover .qr-tooltip {
    opacity: 1;
    visibility: visible;
    transform: translateX(-50%) translateY(-5px);
  }

  /* Animation for tooltip */
  @keyframes tooltipFadeIn {
    from {
      opacity: 0;
      transform: translateX(-50%) translateY(5px);
    }
    to {
      opacity: 1;
      transform: translateX(-50%) translateY(-5px);
    }
  }

  /* Optional: Add a subtle bounce effect */
  @keyframes tooltipBounce {
    0%, 100% {
      transform: translateX(-50%) translateY(-5px);
    }
    50% {
      transform: translateX(-50%) translateY(-8px);
    }
  }

  .qr-tooltip-container:hover .qr-tooltip {
    animation: tooltipFadeIn 0.3s ease forwards,
               tooltipBounce 2s ease infinite 0.3s;
  }

  .custom-number {
    font-size: 1.2rem;
    font-weight: bold;
  }


  /* Optional: Add media query for mobile devices */
  @media (max-width: 768px) {
    .qr-tooltip {
      left: 200%;
    }

    .qr-tooltip-container:hover .qr-tooltip {
      transform: translateX(0) translateY(-5px);
    }

    .qr-tooltip-arrow {
      left: 80px;
      transform: translateX(0);
    }

    .custom-number {
      font-size: 1rem;
    }
  }



</style>
