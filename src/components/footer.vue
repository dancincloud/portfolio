<template>
  <div class="footer fade-content">
    <img class="footer-img" src="assets/icons/footer.png" />
    <div class="media">
      <div
        class="media-item"
        v-for="(item, i) in medias"
        :key="i"
        :src="item.icon"
        @click="openWeb(item.url)"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "web-footer",
  data: () => {
    return {
      medias: [
        {
          name: "email",
          icon: "/assets/icons/media_email.png",
          url:
            "https://mail.google.com/mail/u/0/?view=cm&fs=1&tf=1&source=mailto&to=baijinfan@gmail.com"
        },
        {
          name: "linkedin",
          icon: "/assets/icons/media_linkedin.png",
          url: "https://www.linkedin.com/in/sara-jinfan-bai/"
        },
        {
          name: "ins",
          icon: "/assets/icons/media_ins.png",
          url: "https://www.instagram.com/sarainthesoda/"
        }
      ],
      active: 0
    };
  },
  methods: {
    openWeb(url) {
      window.open(url);
    },
    clickGitHub() {
      window.open("https://github.com/sarabai5");
    }
  }
};
</script>
<style scoped lang="scss">
.footer {
  position: relative;
  display: flex;
  width: 100%;
  height: auto;

  &-img {
    position: relative;
    top: 0;
    left: 0;
    width: 100%;
    height: auto;
  }

  .media {
    position: absolute;
    margin: 248px 0 0 274px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;

    &-item {
      margin: 0 25px 0 0;
      cursor: pointer;
      width: 30px;
      height: 30px;
    }
  }
}
</style>
