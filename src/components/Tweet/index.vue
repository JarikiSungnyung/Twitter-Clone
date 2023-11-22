<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import Icons from '@/components/Icons'

const likeNumber = ref(null)
const reTweetNumber = ref(null)
const replyNumber = ref(null)
const date = ref(null)
const isVideoMode = ref(false)

const userData = ref({
  firstName: null,
  lastName: null,
  pictureUrl: null,
  userId: null
})

const tweetBody = ref({
  content: '',
  author: ''
})

const addLike = () => {
  likeNumber.value += 1
}

const randomUser = async () => {
  const response = await axios.get('https://randomuser.me/api/')
  const value = [...response.data.results][0]
  userData.value.firstName = value.name.first
  userData.value.lastName = value.name.last
  userData.value.pictureUrl = value.picture.medium
  userData.value.userId = value.id.name
}

const getQuote = async () => {
  const response = await axios.get('https://api.quotable.io/random/')
  const data = response.data
  tweetBody.value.content = data.content
  tweetBody.value.author = data.author
}

const setRandomValue = () => {
  let comment = Math.floor(Math.random() * 50) + 1
  let reTweet = Math.floor(comment * 4.3)
  let like = Math.floor(reTweet * 15.7)

  reTweetNumber.value = reTweet
  likeNumber.value = like
  replyNumber.value = comment
  date.value = Math.floor(Math.random() * 24) + 1
}

onMounted(async () => {
  await getQuote()
  await randomUser()
  setRandomValue()

  setTimeout(() => {
    isVideoMode.value = true
  }, 1000)
})
</script>

<template>
  <div id="tweet" v-show="isVideoMode">
    <img :src="userData.pictureUrl" />
    <div class="tweet-content">
      <div class="user-info">
        <p class="name">{{ userData.firstName + ' ' + userData.lastName }}</p>
        <p class="username" v-show="userData.userId">@{{ userData.userId }}</p>
        <span>•</span>
        <p class="date">{{ date }}h</p>
      </div>
      <div class="tweet-body">
        <p>
          {{ tweetBody.content
          }}<span class="hashtag">#{{ tweetBody.author }}</span>
        </p>
      </div>
      <div class="buttons">
        <div class="button" id="reply">
          <icons icon="comment" />
          <span v-show="replyNumber">{{ replyNumber }}</span>
        </div>
        <div class="button" id="retweet">
          <icons icon="retweet" />
          <span v-show="reTweetNumber">{{ reTweetNumber }}</span>
        </div>
        <div class="button" id="like">
          <icons icon="like" />
          <span v-show="likeNumber">{{ likeNumber }}</span>
        </div>
        <div class="button" id="share">
          <icons icon="share" />
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped lang="scss">
#tweet {
  display: flex;
  align-items: flex-start;
  padding: 1rem 31px 11px;
  cursor: pointer;
  border-bottom: 1px solid rgba(0, 0, 0, 0.08);

  &:hover {
    background-color: rgba(0, 0, 0, 0.03);
  }

  img {
    margin-right: 1rem;
    border-radius: 50%;
    width: 48px;
    height: 48px;
  }
  .tweet-content {
    width: 100%;
    .user-info {
      display: flex;
      align-items: flex-start;
      margin-bottom: 11px;
      * {
        margin-right: 4px;
        line-height: 17.58px;
        font-size: 15px;
        color: #828282;
      }
      .name {
        font-weight: 700;
        color: #000;
      }
      span {
        color: #828282;
      }
    }

    .tweet-body {
      margin-bottom: 11px;
      p {
        font-size: 15px;
        line-height: 22px;
        color: #333333;
      }
      .hashtag {
        color: #1da1f2;
      }
      .hashtag:hover {
        text-decoration: underline;
      }
    }

    .buttons {
      display: flex;
      justify-content: space-around;
      width: 100%;
      #reply:hover {
        svg {
          fill: rgba(#1da1f2, 0.8);
          background-color: rgba(#1da1f2, 0.08);
          border-radius: 100px;
        }

        span {
          color: rgba(#1da1f2, 0.8);
        }
      }
      #retweet:hover {
        svg {
          fill: rgba(green, 0.8);
          background-color: rgba(green, 0.08);
          border-radius: 100px;
        }

        span {
          color: rgba(green, 0.8);
        }
      }
      #like:hover {
        svg {
          fill: rgba(red, 0.8);
          background-color: rgba(red, 0.08);
          border-radius: 100px;
        }

        span {
          color: rgba(red, 0.8);
        }
      }
      #share:hover {
        svg {
          fill: rgba(#1da1f2, 0.8);
          background-color: rgba(#1da1f2, 0.08);
          border-radius: 50%;
        }

        span {
          color: rgba(green, 0.8);
        }
      }
      .button {
        display: flex;
        justify-content: center;
        align-items: center;
        svg {
          box-sizing: content-box;
          cursor: pointer;
          width: 18px;
          padding: 0.5rem;
          margin-right: 4px;
        }
        span {
          font-size: 12px;
        }
      }
    }
  }
}

@media (max-width: 476px) {
  #tweet {
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }
}
</style>
