<template>
  <q-page>
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col">
        <q-input
          v-model="newQweetContent"
          class="new-qweet"
          placeholder="무슨 일이 있었나요?"
          counter
          maxlength="280"
          bottom-slots
          :dense="dense"
          autogrow
        >
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://i.ibb.co/WsYvzk6/profile.jpg" />
            </q-avatar>
          </template>
          <template v-slot:append>
            <q-icon
              v-if="newQweetContent !== ''"
              name="close"
              @click="newQweetContent = ''"
              class="cursor-pointer"
            />
          </template>
        </q-input>
      </div>
      <div class="col col-shrink">
        <q-btn
          @click="addNewQweet"
          class="q-mb-lg"
          :disable="!newQweetContent"
          unelevated
          rounded
          color="primary"
          label="크윗"
          no-caps
        />
      </div>
    </div>
    <q-separator class="divider" size="10px" color="grey-2"></q-separator>

    <q-list>
      <q-item v-for="qweet in qweets" :key="qweet.date" class="q-py-md">
        <q-item-section avatar top>
          <q-avatar size="xl">
            <img src="https://i.ibb.co/WsYvzk6/profile.jpg" />
          </q-avatar>
        </q-item-section>

        <q-item-section>
          <q-item-label class="text-subtitle1">
            <strong>주인장</strong>
            <span class="text-grey-7"> @root </span>
          </q-item-label>

          <q-item-label class="qweet-content text-body1"
            >{{ qweet.content }}
          </q-item-label>
          <div class="qweet-icons row justify-between q-mt-sm">
            <q-btn size="sm" flat round color="grey" icon="far fa-comment" />
            <q-btn size="sm" flat round color="grey" icon="fas fa-retweet" />
            <q-btn size="sm" flat round color="grey" icon="far fa-heart" />
            <q-btn
              @click="deleteQweet(qweet)"
              size="sm"
              flat
              round
              color="grey"
              icon="fas fa-trash"
            />
          </div>
        </q-item-section>

        <q-item-section side top>
          {{ Math.round((Date.now() - qweet.date) / 1000 / 60) }}분전
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default {
  name: "PageHome",
  data() {
    return {
      newQweetContent: "",
      qweets: [
        {
          content:
            "만난 사람 모두에게서 무언가를 배울수있는 사람이 세상에서 제일 현명하다.",
          date: 1687419375153,
        },
        {
          content:
            "당신이 가장 많이, 그리고 가장 무거운 거짓말을 전하는 대상은 누구일까요? 머릿속에 수많은 이들이, 특별히 가까운 이들이 스쳐지나가겠지만, 모두 오답입니다. 그리고 당신이 어떤 사람이든 사실 그 답은 똑같습니다. 그 대상은 그 누군가가 아닌 ‘자기 자신’이기 때문입니다.",
          date: 1687409433010,
        },
      ],
    };
  },
  methods: {
    addNewQweet() {
      let newQweet = {
        content: this.newQweetContent,
        date: Date.now(),
      };
      this.qweets.unshift(newQweet);
      this.newQweetContent = "";
    },
    deleteQweet(qweet) {
      let dateToDelete = qweet.date;
      let index = this.qweets.findIndex((qweet) => qweet.date === dateToDelete);
      this.qweets.splice(index, 1);
    },
  },
};
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
