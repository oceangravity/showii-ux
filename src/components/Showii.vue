<template>
  <div class="container">
    <div class="showii-winners-navbar center">
      <img class="icon" src="../assets/cup.png" alt="">
      <img class="icon" src="../assets/see.png" alt="">
      <img class="icon percentage-icon" src="../assets/percentage.png" alt="">
      <img class="icon" src="../assets/star.png" alt="">
    </div>
    <div class="showii-title-info center">
      <span>GANADOS</span>
      <img class="icon" src="../assets/info.png" alt="">
    </div>
    <div class="showii-item-wrapper" v-for="(item, index) in data" :key="index">
      <div class="showii-item-wrapper__header">
        <img class="item-rounded-icon" :src="`http://dev.showii.com/sw-manager/pics_users/${item.product.branch.photo[0]}_thumb.jpg`" alt="">
        <span class="showii-item-wrapper__title">{{item.product.branch.name}}</span>
      </div>
      <div class="showii-item-wrapper__body">
        <div>
          <img class="item-rounded-icon" :src="`//dev.showii.com/sw-manager/pics_prods/${item.product.photo[0]}_thumb.jpg`" alt="">
        </div>
        <div>
          <span class="showii-item-wrapper__body-content">{{item.product.shortDescription}}</span>
        </div>
      </div>
      <div class="showii-item-wrapper__footer">
        <span class="showii-item-wrapper__footer--date">{{formatDate(item.product.endDate)}}</span>
        <span class="showii-item-wrapper__footer--icons">
          <img class="icon" src="../assets/qr.png" alt="">
          <img class="icon" src="../assets/edit.png" alt="">
          <img class="icon" src="../assets/delete.png" alt="">
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  data () {
    return {
      loading: false,
      data: []
    }
  },
  mounted () {
    this.loading = true
    axios
      .get('http://dev.showii.com/servicesshowii/public/index.php/api/v4/awards', {
        headers: { 'Authorization': 'LT 45kblk8RjuKNJIfG3R6K5i8Z9R8Vi0K3wi2lElqpqQD0veNINR' }
      })
      .then(response => {
        this.data = response.data.p
        console.log(JSON.parse(JSON.stringify(response.data)))
        this.loading = false
      })
  },
  methods: {
    formatDate (unixTimestamp) {
      let date = new Date(unixTimestamp * 1000)
      let options = {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      }

      return date.toLocaleDateString('es-ES', options)
        .replace(/de /g, '')
    }
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Poppins:300,400,500');
  // @import './styles/custom-bootstrap.scss';
  @import '/~bootstrap/scss/bootstrap';

  body {
    font-family: 'Poppins', sans-serif;
    color: #909090;
  }

  .container {
    max-width: 468px;
  }

  .percentage-icon {
    height: 24px;
    width: auto !important;
  }

  .showii-winners-navbar {
    padding: 10px 0;

    .icon {
      width: 24px;
      margin: 20px 30px;
    }
  }

  .showii-title-info {
    padding: 10px 0;

    .icon {
      width: 24px;
      float: right;
    }
  }

  .showii-item-wrapper {
    padding-top: 30px;
  }

  .showii-item-wrapper::after {
    border-bottom: solid 1px;
    content: '';
    position: absolute;
    width: 100%;
    height: 1px;
    left: 0;
    opacity: 0.3;
  }

  .self-center {
    margin-left: auto;
    margin-right: auto;
  }

  .center {
    text-align: center;
  }

  .item-rounded-icon {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin-right: 15px;
    border: solid 1px rgba(144, 144, 144, 0.2);
  }

  .showii-title-info {
    position: relative;
    line-height: 26px;
    height: 44px;

    .icon {
      position: absolute;
      right: 0;
    }
  }

  .showii-item-wrapper__header {
    display: inline-block;
    height: auto;
    width: 100%;
    line-height: 40px;
    margin-bottom: 10px;
  }

  .showii-item-wrapper__body {
    display: inline-block;
    height: auto;
    margin-bottom: 10px;

    .showii-item-wrapper__body-content {
      font-weight: 300;
      display: block;
      height: 50px;
      overflow: hidden;
      position: relative;

      &::before {
        content: '...More';
        position: absolute;
        background-color: #fff;
        bottom: 2px;
        right: 0;
        width: 61px;
        z-index: 1;
        font-weight: 500;
        text-align: center;
        padding-left: 2px;
      }

    }

    > div {
      display: table-cell;
      vertical-align: top;

      .showii-item-wrapper__title {
        height: auto;
      }
    }
  }

  .showii-item-wrapper__title {
    height: 40px;
    line-height: 42px;
    display: inline-block;
    vertical-align: middle;
    font-weight: 500;
  }

  .showii-item-wrapper__footer {
    position: relative;
    height: 30px;
    line-height: 30px;
    margin-bottom: 15px;

    > .showii-item-wrapper__footer--icons {
      position: absolute;
      right: 0;
      top: 0;
    }

    > .showii-item-wrapper__footer--date {
      line-height: 31px;
      text-transform: uppercase;
    }

    .icon {
      width: 24px;
      margin: 0 0 0 25px;
      display: inline-block;
    }
  }

</style>
