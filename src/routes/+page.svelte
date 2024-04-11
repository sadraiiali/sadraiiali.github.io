<script>
  import SlidePanel from "$lib/SlidePanel.svelte";
  import Avatar from "$lib/Avatar.svelte";
  import NameTag from "$lib/NameTag.svelte";

  let socialLinks = [
    {
      link: "https://keybase.io/sadraiiali",
      icon: "img/socials/keybase.svg",
      alt: "keybase",
    },
    {
      link: "https://t.me/thepiker",
      icon: "img/socials/telegram.svg",
      alt: "telegram",
    },
    {
      link: "https://mastodon.social/web/accounts/1074221",
      icon: "img/socials/mastodon.svg",
      alt: "mastodon",
    },
    {
      link: "https://instagram.com/sadraiiali",
      icon: "img/socials/instagram.svg",
      alt: "instagram",
    },
    {
      link: "https://soundcloud.com/ali-sadraei",
      icon: "img/socials/soundcloud.png",
      alt: "soundcloud",
    },
    {
      link: "mailto://sadraiiali@gmail.com",
      icon: "img/socials/mail.svg",
    },
  ];
</script>

<SlidePanel>
  <div
    class="flex flex-row gap-2 w-full h-full justify-center items-center"
    slot="content"
  >
    <div class="flex flex-col info gap-2">
      <!-- <img
            src="img/alireza-sadraii.jpg"
            class="photo"
            alt="alireza sadraii rad"
          /> -->

      <Avatar />
      <NameTag />
    </div>

    <div class="links">
      {#each socialLinks as s, i}
        <a href={s.link} target="_blank" rel="noopener noreferrer">
          <img
            src={s.icon}
            alt={s.alt}
            class="social-icon"
            height="20"
            width="20"
          />
        </a>
      {/each}
    </div>
  </div>
</SlidePanel>

<style lang="scss">
  .links {
    touch-action: none;

    @apply flex flex-col gap-2 border-2 border-gray-500 h-[19rem] w-10 px-2 justify-center;
  }

  .photo {
    touch-action: none;

    @apply border-2 border-gray-500 w-60;
  }
</style>
