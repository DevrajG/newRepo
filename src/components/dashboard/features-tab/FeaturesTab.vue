<template>
  <div class="overview-tab dashboard-tab">
    <div class="d-flex overview-row flex-row w-100 justify-content-sm-around justify-content-xs-start">

      <div class="overview-col">
        <div class="overview-item">
          <div class="overview-icon-container">
            <i class="i-vuestic-vue"></i>
          </div>
          Built with Vue.js framework
        </div>
        <div class="overview-item">
          <div class="overview-icon-container">
            <i class="i-icon-faster text-secondary"></i>
          </div>
          Absolutely free for everyone
        </div>
        <div class="overview-item">
          <div class="overview-icon-container">
            <i class="i-icon-updown"></i>
          </div>
          Fresh and crisp design
        </div>
      </div>

      <div class="overview-col">
        <div class="overview-item">
          <div class="overview-icon-container">
            <i class="i-vuestic-responsive"></i>
          </div>
          Responsive and optimized for mobile
        </div>
        <div class="overview-item">
          <div class="overview-icon-container">
            <i class="i-vuestic-rich"></i>
          </div>
          Tons of useful components
        </div>
        <div class="overview-item">
          <div class="overview-icon-container">
            <i class="i-icon-updown"></i>
          </div>
          Completely jQuery free
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'features-tab',
  created () {
    this.initalization()
  },

  data () {
    return {
      statsDatas: []
    }
  },

  methods: {
    async initalization () {
      const me = this.$store.getters['account/myself']
      try {
        const { userId, accessToken } = me
        const { error, stats } = await new Proxy('getStats.php?', {
          userId,
          accessToken
        }).submit('get')
        if (error) {
          this.statsDatas = []
        } else {
          this.statsDatas = stats
          this.isLoaded = true
        }
      } catch (error) {
        this.$store.dispatch('auth/notification', {
          type: 'ERROR',
          title: 'SERVER ERROR',
          message: 'Oops, Please try again later.'
        })
      }
    },

  },
}
</script>

<style lang="scss" scoped>
.overview-item {
  display: flex;
  align-items: center;
  height: 55px;
  margin-bottom: 3rem;
  padding-right: 1rem;
  font-size: 1.25rem;
  font-weight: bold;

  .overview-icon-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    min-width: 85px;
    max-width: 85px;
    height: 100%;
  }
}

.overview-row {
  @include media-breakpoint-down(xs) {
    flex-wrap: wrap;
  }
}

.overview-col:first-child {
  margin-left: 2rem;
  @include media-breakpoint-down(md) {
    margin-left: 0;
  }
}

.explore-btn {
  margin-top: 6rem;
  margin-bottom: 1rem;
}
</style>
