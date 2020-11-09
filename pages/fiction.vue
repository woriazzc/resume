<template>
  <div>
    <Collapse accordion>
      <Panel v-for="item in fiction" :key="item.id" :name="item.title">
        <Rate :value="parseInt(item.rate)" disabled />
        {{ item.title }}
        <Tag
          v-if="item.status === 'done'"
          color="success"
          :style="{ margin: '0 10px 0 10px' }"
        >
          {{
            item.date === null
              ? $t('fiction.done')
              : $t('fiction.done_at', { date: item.date })
          }}
        </Tag>
        <Tag
          v-if="item.status === 'doing'"
          color="primary"
          :style="{ margin: '0 10px 0 10px' }"
        >
          {{ $t('fiction.doing') }}
        </Tag>
        <Tag
          v-if="item.status === 'todo'"
          color="error"
          :style="{ margin: '0 10px 0 10px' }"
        >
          {{ $t('fiction.todo') }}
        </Tag>
        <Tag
          v-for="leb in splitToArray(item.label)"
          :key="leb"
          :color="randomLabelColor()"
        >
          {{ leb }}
        </Tag>
        <p slot="content">
          {{ item.comment }}
        </p>
      </Panel>
    </Collapse>
  </div>
</template>

<script>
import { fiction } from 'assets/reader'
import { splitToArray, randomLabelColor } from 'assets/util'

export default {
  name: 'Fiction',
  data() {
    return {
      fiction,
      splitToArray,
      randomLabelColor,
    }
  },
  mounted() {
    this.$Message.info(this.$t('fiction.message'))
    this.$Message.error({
      content: this.$t('fiction.warning'),
      duration: 5,
      closable: true,
    })
  },
}
</script>