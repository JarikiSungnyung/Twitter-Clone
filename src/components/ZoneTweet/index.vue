<script setup>
import Icons from '@/components/Icons'
</script>

<template>
  <div id="zone-tweet">
    <img
      src="data:image/jpeg;base64,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"
      class="avatar-image"
    />
    <div class="input-context">
      <input type="text" placeholder="What's happening" />
      <div class="icons">
        <div class="left-icon">
          <icons icon="image" />
          <icons icon="gif" />
          <icons icon="Stats" />
          <icons icon="smile" />
          <icons icon="schedule" />
        </div>
        <div class="right-icon">
          <button>Tweet</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
#zone-tweet {
  border-top: 1px solid rgba(0, 0, 0, 0.08);
  border-bottom: 1px solid rgba(0, 0, 0, 0.08);
  width: 600px;
  padding-left: 1rem;
  padding-top: 8px;
  display: flex;
  align-items: flex-start;
  img {
    margin-right: 1rem;
  }
  img.avatar-image {
    margin-right: 1rem;
    border-radius: 50%;
    width: 48px;
    height: 48px;
  }
  .input-context {
    margin-right: 2rem;
    display: flex;
    flex-direction: column;
    flex: 1;

    input {
      color: #828282;
      font-weight: 400;
      line-height: 22.27px;
      font-size: 19px;
      padding: 1rem 1rem 40px 1rem;
    }
    input:active {
      outline: none;
      border: none;
    }
    input:focus {
      outline: 0;
    }

    .icons {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 22px;
      .left-icon {
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;

        svg {
          border-radius: 50%;
          padding: 0.5rem;
          box-sizing: content-box;
          &:hover {
            background-color: rgba(#1da1f2, 0.1);
          }
        }
      }

      .right-icon {
        display: flex;
        align-items: center;
        justify-content: center;
        button {
          margin-right: 0px;
          background-color: #1da1f2;
          width: 98px;
          height: 42px;
          border-radius: 100px;
          font-weight: 700;
          font-size: 15px;
          line-height: 17.58px;
          cursor: pointer;
          color: #fff;
          transition: 1s color, 1s background-color;
        }
        button:hover {
          color: #1da1f2;
          background-color: #fff;
          border: 1px solid #1da1f2;
        }
        button:active {
          outline: none;
          border: none;
        }
        button:focus {
          outline: 0;
        }
      }
    }
  }
}

@media (max-width: 758px) {
  #zone-tweet {
    width: 100%;
  }
}

@media (max-width: 476px) {
  #zone-tweet {
    display: none;
  }
}
</style>
