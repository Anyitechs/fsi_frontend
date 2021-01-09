<template>
  <div class="home">
    <div class="navigation">
      <router-link to="/">
      <img src="../assets/images/fsi_logo.jpg" alt="FSI Logo" class="navigation__logo">
      </router-link>
      <nav class="navigation__nav">
        <ul class="navigation__list">
          <li class="navigation__item">
            <a href="/" class="navigation__link active">Home</a>
          </li>
          <li class="navigation__item"><a href="#services" class="navigation__link">Health plans</a></li>
        </ul>
      </nav>
    </div>
    <main>
      <section class="heading-section">
        <div class="heading">
          <div class="heading__text">
            <h3 class="heading__text--title">Find the right health <br> insurance plan for you</h3>
            <p class="heading__text--sub">FSI Health helps you find best health insurance plans. <br> 
                We compare more than 1000 health insurance <br>
                products across 300+ deals and provide single <br>
                platform to buy, renew or choose your health <br>
                insurance plan.
            </p>
            <button @click="verifyBVN" class="btn btn-primary">Get started</button>
          </div>
          <div class="heading__image">
            <img src="../assets/images/trafalgar-header-illustration.png" alt="Heading Illustration">
          </div>
        </div>
      </section>
      <Services />
      <Footer />
    </main>
  </div>
</template>

<script>
import axios from "axios";
import Services from "./Services.vue";
import Footer from "./Footer.vue";
export default {
  data () {
    return {
      credentials: null
    };
  },
  components: { 
    Services,
    Footer
  },
  name: "Home",
  methods: {
    async verifyBVN() {
        const response = await axios.post("https://fsibackend.herokuapp.com/api/v1/bvn/reset");
        if (response.data.success) {
          this.credentials = response.data.requestCredentials;
          sessionStorage.setItem("credentials", JSON.stringify(this.credentials));
          console.log('credentials')
          console.log(this.credentials)
          this.$router.push("/signup");
        } else {
          this.$router.push("/");
        }
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  .navigation {

    &__list {
      float: right;
      margin-right: 15rem;
      margin-top: -9rem;
    }
    &__item {
      margin-left: 2rem;
      display: inline-block;
      list-style: none;
    }
    &__logo {
      margin-left: 8rem;
      max-width: 10%;
    }
    &__link {
      &:link,
      &:visited {
        text-decoration: none;
        color: $color-gray;
        font-size: 1.6rem;
      }

      &:hover,
      &.active {
        color: $color-primary;
      }
    }
  }
  .heading {
    margin-top: 1rem;
    margin-left: 4rem;
    display: grid;
    align-items: center;
    grid-template-columns: repeat(auto-fit, minmax(24rem, 1fr));

    &__text {
      margin-left: 8rem;

      &--title {
        padding-bottom: 4rem;
        line-height: 1.3;
        color: $color-black;
        font-size: 4rem;
        font-weight: 700;
      }

      &--sub {
        font-size: 1.9rem;
        padding-bottom: 4rem;
      }
    }

    &__image > img {
      max-width: 100%;
    }
  }
  .btn {
    border: none;
    cursor: pointer;
    border-radius: 10rem;
    background-color: $color-primary;
    padding: 1.5rem 4.5rem;
    color: $color-white;
    font-size: 1.8rem;
    transition: all .3s;

    &:hover {
      transform: scale(1.05);
      background-color: lighten($color-primary, 10%);
    }
  }
}
@media only screen 
  and (min-device-width: 320px) 
  and (max-device-width: 667px) 
  and (-webkit-min-device-pixel-ratio: 2) { 
    .home {
      .navigation {
        box-shadow: 0px 4px 10px -6px rgba(120, 120, 118, 0.25);

        &__logo {
          margin-left: -4rem;
          margin-top: -4rem;
          max-width: 50%;
          position: relative;
        }
        &__item {
          display: inline-block;
          list-style: none;
          position: absolute;
          left: 18rem;
          top: 5rem;
        }
        &__link {
          &:link,
          &:visited {
            text-decoration: none;
            color: $color-gray;
            font-size: 2.5rem;
          }

          &.active {
            visibility: hidden;
          }
        }
      }

      .heading {
        margin-top: 1rem;
        margin-left: -7rem;
        display: grid;
        align-items: center;
        grid-template-columns: repeat(1, 1fr);

        &__text {

          &--title {
            padding-bottom: 4rem;
            line-height: 1.3;
            color: $color-black;
            font-size: 4rem;
            font-weight: 700;
          }

          &--sub {
            font-size: 1.9rem;
            padding-bottom: 4rem;
          }

          br {
            display: none;
          }
        }

        &__image > img {
          max-width: 100%;
          margin-top: 4rem;
          margin-left: 2rem;
        }
      }
    }

}
</style>
