<template>
  <Layout>
    <div class="tags">
      <router-link  class="tag"
                    v-for="tag in tags" :key="tag.id"
                    :to="`/labels/edit/${tag.id}`">
        <span>{{ tag.name }}</span>
        <icon name="right"/>
      </router-link>
    </div>
    <div class="createTag-wrapper">
      <Button @click="createTag">新增标签</Button>
    </div>
  </Layout>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';
import tagListModel from '@/models/tagListModel';
import Button from '@/components/Button.vue';

tagListModel.fetch();
@Component({
  components: {Button}
})
export default class Labels extends Vue {
  tags = window.tagList;

  createTag() {
    const name = window.prompt('请输入标签名');
    if (name) {
      const message = tagListModel.create(name);
      if (message === 'duplicated') {
        window.alert('标签名已存在');
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.tags {
  background: white;
  padding-left: 16px;
  font-size: 16px;

  .tag {
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid #e6e6e6;
    min-height: 44px;

    svg {
      margin-right: 14px;
      width: 18px;
      height: 18px;
      color: #666;
    }
  }
}

.createTag-wrapper {
  text-align: center;
  padding: 16px;
  margin-top: 44-16px;
}
</style>