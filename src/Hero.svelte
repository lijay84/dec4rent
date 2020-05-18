<script>
  export let heroProps;
</script>

<style type="text/scss">
  .hero {
    height: 400px;
    background-position: left 70%;
    background-size: cover;
    left: 0;
    right: 0;
    margin-bottom: 100px;
    display: flex;
    font-family: "Roboto Condensed", sans-serif;
    .text {
      margin: 3% 20%;
      width: 50%;
      text-transform: uppercase;
      font-weight: 700;
      position: relative;
      .title {
        color: #fff !important;
        width: 72%;
        font-size: 80px;
        font-style: italic;
        line-height: 80px;
        padding-bottom: 20px;
        text-shadow: 3px 2px rgba(0, 0, 0, 0.5);
      }
      .subtitle {
        color: #fff !important;
        font-size: 22px;
        line-height: 29px;
        text-shadow: 3px 2px rgba(0, 0, 0, 0.5);
      }
      .offer {
        display: flex;
        position: absolute;
        left: 50%;
        top: 41%;
        flex-direction: column;
        .yellow-evidence {
          height: 50px;
          width: 200px;
          margin-bottom: 3px;
          transform: rotate(-5deg);
          background-color: #feed00;
          color: #1a171b;
          font-size: 24px;
          font-weight: 700;
          display: inline-flex;
          justify-content: center;
          align-items: center;
          text-transform: uppercase;
          &:last-child {
            margin-left: 50px;
          }
        }
      }
    }
  }
  @media (max-width: 575px) {
    .hero {
      .text {
        margin: 20px;
        margin-top: 37%;
        width: 100%;
        .title {
          font-size: 40px;
          line-height: 50px;
          width: 100%;
          padding-bottom: 0;
        }
        .subtitle {
          font-size: 20px;
          line-height: 27px;
        }

        .offer {
          top: auto;
          left: 22%;
          .yellow-evidence {
            height: 30px;
            line-height: 16px;
            font-size: 17px;
            width: 140px;
          }
        }
      }
    }
  }
  @media (max-width: 991px) and (min-width: 768px) {
    .hero {
      .text {
        margin: 3% 7%;
        width: 100%;
        .title {
          padding-top: 80px;
          padding-bottom: 76px;
          font-size: 60px;
          line-height: 50px;
        }
        .offer {
          right: 0;
          left: auto;
          top: 41%;
        }
      }
    }
  }
  @media (max-width: 1366px) and (min-width: 992px) {
    .hero {
      .text {
        margin: 4% 4%;
        width: 100%;
        .title {
          padding-bottom: 100px;
          font-size: 60px;
          line-height: 50px;
          width: 320px;
        }
        .offer {
          right: 0;
          left: auto;
          top: 25%;
        }
      }
    }
  }
</style>

<div style="background-image: url('{heroProps.bgImage}')" class="hero">
  <div class="text">
    <div class="title">{heroProps.title}</div>
    <div class="subtitle">{heroProps.subtitle}</div>
    <div class="offer">
      <div class="yellow-evidence">risparmia fino</div>
      <div class="yellow-evidence">al -{heroProps.discount}%</div>
    </div>
  </div>
</div>
