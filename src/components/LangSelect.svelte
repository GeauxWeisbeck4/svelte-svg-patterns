<script>
  import { langStore } from "../routes/stores.js";
  import lang from "../routes/_lang.js";
  let strings = lang.strings;
  let toClose = false;

  let language = $langStore || "en";
  let languageList = [
    { id: "en", name: "English", link: "https://pattern.monster" },
    { id: "de", name: "Deutsch", link: "https://de.pattern.monster" },
    { id: "es", name: "Español", link: "https://es.pattern.monster" },
    { id: "fr", name: "Français", link: "https://fr.pattern.monster" },
    { id: "it", name: "Italiano", link: "https://it.pattern.monster" },
    { id: "nl", name: "Nederlands", link: "https://nl.pattern.monster" },
    { id: "pl", name: "Polski", link: "https://pl.pattern.monster" },
    { id: "pt", name: "Português", link: "https://pt.pattern.monster" },
    { id: "ro", name: "Română", link: "https://ro.pattern.monster" },
    { id: "sv", name: "Svenska", link: "https://sv.pattern.monster" },
    { id: "tr", name: "Türkçe", link: "https://tr.pattern.monster" },
    { id: "ar", name: "العربية", link: "https://ar.pattern.monster" },
    { id: "zh-cn", name: "中文(简体)", link: "https://cn.pattern.monster" },
  ];

  const languageName = languageList.find(({ id }) => id === language).name;

  function toggle(e) {
    e.stopPropagation();
    let menu = this.nextSibling;
    // let menu = document.getElementById('langMenu')
    document.getElementById('shopMenu').style.display = "none";

    while (menu && menu.nodeType != 1) {
      menu = menu.nextSibling;
    }
    if (!menu) return;
    if (menu.style.display !== "block") {
      menu.style.display = "block";
      if (toClose) toClose.style.display = "none";
      toClose = menu;
    } else closeAll();
  }
  function closeAll() {
    toClose.style.display = "none";
    toClose = false;
  }

  function closeWindow(event) {
    if (toClose) closeAll.call(event.target);
  }
</script>

<!-- https://codepen.io/vlastapolach/pen/EXdLMy -->
<svelte:window on:click={closeWindow} />

<div class="menu">
  <button class="menuButton flex items-center" title={strings.translate} on:click={toggle}>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="2em"
      height="2em"
      viewBox="0 0 24 24"
      stroke-width="1.5"
      stroke="currentColor"
      fill="none"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <path d="M5 7h7m-2 -2v2a5 8 0 0 1 -5 8m1 -4a7 4 0 0 0 6.7 4" />
      <path d="M11 19l4 -9l4 9m-.9 -2h-6.2" />
    </svg>
    <span class="dropDownName">{languageName}</span>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="1.5em"
      height="1.5em"
      viewBox="0 0 24 24"
      stroke-width="1.5"
      stroke="currentColor"
      fill="none"
      stroke-linecap="round"
      stroke-linejoin="round"
    >
      <polyline points="6 9 12 15 18 9" />
    </svg>
  </button>
  <ul id="langMenu" class="menuItems p-0">
    {#each languageList as lang}
      <li>
        <a class="px-4 py-3 {lang.name === languageName ? 'selectedLang' : ''}" href={lang.link}>{lang.name}</a>
      </li>
    {/each}
    <li class="translateLink"><a class="px-4 py-3" href="https://crwd.in/pattern-monster" target="_blank">{strings.translate}</a></li>
  </ul>
</div>

<style>
  .menu {
    display: grid;
    margin: 0 auto;
    justify-items: end;
    font-size: 1em;
  }
  .translateLink {
    border-top: 2px solid var(--secondary-color);
  }

  /* .menu:focus,
  .menu:active {
    outline: 1px solid #fff; */
  /* outline-offset: -4px; */
  /* } */
  /* .menu:hover {
    border-radius: var(--border-radius);
    background-color: var(--gray-800);
  } */
  .menuButton {
    font-weight: 500;
    border-radius: var(--border-radius);
  }
  .menuButton > span {
    padding: 0 0.5em;
  }
  .menuButton:hover {
    border-radius: var(--border-radius);
    background-color: var(--gray-800);
  }
  .menuButton:active,
  .menuButton:focus {
    /* outline: none; */
    background-color: var(--gray-800);
    outline: 1px solid #fff;
  }

  .menuItems {
    z-index: 20;
    overflow-y: auto;
    max-height: 75vh;
    display: none;
    min-width: 160px;
    margin-top: 3em;
    position: fixed;
    list-style: none;
    background-color: var(--main-bg-color);
    border: 1px solid var(--main-bg-color);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
    -webkit-background-clip: padding-box;
    background-clip: padding-box;
    border-radius: var(--border-radius);
    box-shadow: 0 10px 15px -3px rgb(0 0 0 / 10%), 0 4px 6px -2px rgb(0 0 0 / 5%);
    /* --tw-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
    --tw-ring-offset-shadow: 0 0 #0000;
    box-shadow: var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow); */
    /* padding: 0; */
  }
  .menuItems a {
    text-decoration: none;
    /* padding: 0; */
  }
  .menuItems li a {
    color: var(--gray-300);
  }
  .menuItems li a.selectedLang {
    color: var(--secondary-color);
    background-color: var(--gray-800);
  }
  .menuItems li a:hover {
    background-color: var(--gray-700);
  }
</style>
