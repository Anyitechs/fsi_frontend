<template>
  <div class="services">
      <div class="services__text">
        <h3 class="services__text--title">Our services</h3>
        <span class="services__text--footnote">.</span>
        <p class="services__text--sub">Compare Health Insurance Plans to get the right health cover for you and your family. 
            Use our service to compare various health insurance plans, 
            choose the right one and buy online.
        </p>
      </div>
      <div class="services__list" v-if="plans">
          <div class="services__card">
              <div class="services__price">
                  <p> #{{ plans.plans[0].price.monthly }} /Monthly </p>
              </div>
              <img src="../assets/images/individual.png" alt="Individual Health Plan">
               <h3> {{ plans.plans[0].name }} </h3>
              <div class="services__card--details">
                  <ul v-for="plan in plans.plans[0].summary" :key="plan.name">
                      <li> {{ plan.name }} - {{ plan.value }} </li>
                  </ul>
              </div>
          </div>
          <div class="services__card">
              <div class="services__price">
                  <p> #{{ plans.plans[0].price.quarterly }} /Quarterly </p>
              </div>
              <img src="../assets/images/couples.png" alt="Couples Health Plan">
               <h3> {{ plans.plans[0].name }} </h3>
              <div class="services__card--details">
                  <ul v-for="plan in plans.plans[0].summary" :key="plan.name">
                      <li> {{ plan.name }} - {{ plan.value }} </li>
                  </ul>
              </div>
          </div>
          <div class="services__card">
              <div class="services__price">
                  <p> #{{ plans.plans[0].price.yearly }} /Yearly </p>
              </div>
              <img src="../assets/images/family.png" alt="Family Health Plan">
               <h3> {{ plans.plans[0].name }} </h3>
              <div class="services__card--details">
                  <ul v-for="plan in plans.plans[0].summary" :key="plan.name">
                      <li> {{ plan.name }} - {{ plan.value }} </li>
                  </ul>
              </div>
          </div>
      </div>
      <div class="services__subscribe">
          <button @click="verifyBVN" class="btn">Sign up</button>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Services',
    data () {
        return {
            plans: null,
            credentials: null
        }
    },
    created() {
        axios.get('https://fsibackend.herokuapp.com/api/v1/plans').then(response => {
            this.plans = response.data.plans
        }).catch(error => {
            console.log(error);
        })
    },
    methods: {
        async verifyBVN() {
            const response = await axios.post('https://fsibackend.herokuapp.com/api/v1/bvn/reset')
            if (response.data.success) {
            this.credentials = response.data.requestCredentials;
            sessionStorage.setItem('credentials', JSON.stringify(this.credentials));
            console.log('credentials')
            console.log(this.credentials)
            this.$router.push('/signup');
            } else {
            this.$router.push('/');
            }
        }
    }
}
</script>

<style lang="scss">
.services {
    margin-top: 12rem;

    &__price {
        margin-left: 18rem;
        position: relative;
        top: 7rem;

        p {
            font-size: 2rem;
            font-weight: 700;
            font-style: italic;
        }
    }
    &__text {
        
        &--title {
            text-align: center;
            color: $color-black;
            font-size: 3.5rem;
            font-weight: 700;
        }

        &--footnote {
            border-top: 2px solid $color-black;
            padding: 1rem 2.8rem;
            position: relative;
            left: 62rem;
            top: 2.5rem;
        }

        &--sub {
            text-align: center;
            font-size: 1.9rem;
            padding: 4rem 20rem;
        }
    }

    &__list {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
        grid-gap: .5rem;
    }

    &__card {
        height: auto;
        width: 80%;
        border-radius: 2rem;
        box-shadow: 0 1.5rem 4rem rgba($color-black, .15);
        margin-top: 4rem;
        margin-left: 4rem;
        margin-right: 4rem;
        transition: all .3s;

        
        &--details {
            padding: 1rem;

            ul {
                list-style: none;
                width: 80%;
                margin: 0 auto;

                li {
                    text-align: center;
                    font-size: 1.2rem;
                    font-weight: 700;
                    padding: 1rem;
                    border-bottom: 1px solid $color-grey-light;
                }
            }
        }
      

        &:hover {
            transform: scale(1.05);
        }

        img {
            max-width: 50%;
        }

        h3 {
            padding-left: 2rem;
            font-size: 1.8rem;
            font-weight: 700;
            color: $color-black;
        }
    }

    &__subscribe {
        margin-top: 8rem;
        margin-left: 58rem;
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
      .services {
          margin-top: 6rem;

          &__text {

            &--title {
                text-align: center;
                color: $color-black;
                font-size: 3.5rem;
                font-weight: 700;
            }

            &--footnote {
                border-top: 2px solid $color-black;
                padding: 1rem 2.8rem;
                position: relative;
                left: 13rem;
                top: 1rem;
            }

            &--sub {
                padding: 0;
                position: relative;
                top: 2rem;
                font-size: 1.9rem;
            }
          }
        &__list {
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
                grid-gap: .5rem;
            }

            &__card {
                height: auto;
                width: 100%;
                border-radius: 2rem;
                box-shadow: 0 1.5rem 4rem rgba($color-black, .15);
                margin-top: 8rem;
                margin-left: -.3rem;
                // margin-right: 4rem;
                transition: all .3s;

                &:hover {
                    transform: scale(1.05);
                }

                img {
                    max-width: 50%;
                }

                h3 {
                    padding-left: 2rem;
                    font-size: 1.8rem;
                    font-weight: 700;
                    color: $color-black;
                }
            }

            &__subscribe {
                margin-top: 5rem;
                margin-left: 8.5rem;
            }
      }
  }
</style>