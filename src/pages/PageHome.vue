<template>
  <q-page>
    <div class="q-py-lg q-px-md row items-end
    q-col-gutter-md">
      <div class="col">
        <q-input
        v-model="newQweetContent"
        class="new-qweet"
        placeholder="무슨 일이 있었나요?"
        counter maxlength="280"
        bottom-slots
        :dense="dense"
        autogrow
        >
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://i.ibb.co/WsYvzk6/profile.jpg">
            </q-avatar>
          </template>
          <template v-slot:append>
            <q-icon v-if="newQweetContent !== ''" name="close" @click="newQweetContent = ''" class="cursor-pointer" />
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">
            <q-btn
            @click="addNewQweet"
            class="q-mb-lg"
            :disable="!newQweetContent"
            unelevated rounded
            color="primary"
            label="크윗"
            no-caps
            />
      </div>
    </div>
    <q-separator
      class="divider"
      size="10px"
      color="grey-2"></q-separator>

      <q-list>
      <q-item
        v-for="qweet in qweets"
        :key="qweet.date"
        class="q-py-md"
      >
        <q-item-section avatar top>
          <q-avatar size="xl">
              <img src="https://i.ibb.co/WsYvzk6/profile.jpg">
            </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-subtitle1">
            <strong>크위터</strong>
            <span class="text-grey-7">
              @qwitter
            </span>
          </q-item-label>

          <q-item-label class="qweet-content text-body1">{{ qweet.content }}
          </q-item-label>
          <div class="qweet-icons row justify-between q-mt-sm">
            <q-btn
            size="sm"
            flat
            round
            color="grey"
            icon="far fa-comment" />
            <q-btn
            size="sm"
            flat
            round
            color="grey"
            icon="fas fa-retweet" />
            <q-btn
            size="sm"
            flat
            round
            color="grey"
            icon="far fa-heart" />
            <q-btn
            size="sm"
            flat
            round
            color="grey"
            icon="fas fa-trash" />
          </div>
        </q-item-section>

        <q-item-section side top>
          {{ Math.round((Date.now() - qweet.date)/1000/3600) }}시간전
        </q-item-section>
      </q-item>

    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default{
  name: 'PageHome',
  data(){
    return {
      newQweetContent: '',
      qweets: [
        {
          content: 'Lorem Ipsum은 단순히 인쇄 및 조판 업계의 더미 텍스트입니다. Lorem Ipsum은 1500년대 이후 업계의 표준 더미 텍스트였습니다. 알 수 없는 인쇄업자가 활자 갤리를 가져와 활자 표본 책을 만들기 위해 뒤섞었습니다. 그것은 5세기 동안 살아남았을 뿐만 아니라 전자식 조판으로의 도약에도 본질적으로 변하지 않았습니다. 1960년대에 Lorem Ipsum 구절이 포함된 Letraset 시트의 출시와 함께 대중화되었으며, 최근에는 Lorem Ipsum 버전을 포함하는 Aldus PageMaker와 같은 데스크탑 출판 소프트웨어로 대중화되었습니다.',
          date: 1687419375153,
        },
        {
          content: 'Lorem Ipsum은 단순히 인쇄 및 조판 업계의 더미 텍스트입니다. Lorem Ipsum은 1500년대 이후 업계의 표준 더미 텍스트였습니다. 알 수 없는 인쇄업자가 활자 갤리를 가져와 활자 표본 책을 만들기 위해 뒤섞었습니다. 그것은 5세기 동안 살아남았을 뿐만 아니라 전자식 조판으로의 도약에도 본질적으로 변하지 않았습니다. 1960년대에 Lorem Ipsum 구절이 포함된 Letraset 시트의 출시와 함께 대중화되었으며, 최근에는 Lorem Ipsum 버전을 포함하는 Aldus PageMaker와 같은 데스크탑 출판 소프트웨어로 대중화되었습니다.',
          date: 1687409433010,
        },
      ],
    }
  },
  methods: {
    addNewQweet() {
      let newQweet = {
        content: this.newQweetContent,
        date: Date.now()
      }
      this.qweets.unshift(newQweet)
      this.newQweetContent = ''
    }
  }
}
</script>
<style lang="sass">
.new-qweet
  textarea
    font-size: 19px
    line-height: 1.4 !important

.divider
  border-top: 1px solid
  border-bottom: 1px solid
  border-color: $grey-4

.qweet-content
  white-space: pre-line

.qweet-icons
  margin-left: -5px
</style>
