<template>
  <p>{{ lang[selected].root }}</p>
  <p>{{ lang[selected].title }}</p>
  <button
    v-for="(item, i) in data.languages"
    :key="i"
    @click="selectLang(item.key)"
  >
    {{ item.value }}
  </button>
  <p>{{ lang[selected].selected }} {{ selectedValue }}</p>
</template>
<script lang="ts">
import { reactive, ref, computed } from "vue";
export default {
  name: "Grammar",
  setup() {
    const data = reactive({
      languages: [
        { key: "zh-cn", value: "简体中文" },
        { key: "zh-tw", value: "繁体中文" },
        { key: "us", value: "English" },
      ],
    });
    const lang = reactive({
      "zh-cn": {
        root: "多个根节点",
        title: "Setup函数",
        selected: "选择的项：",
      },
      "zh-tw": {
        root: "多個根節點",
        title: "Setup函數",
        selected: "選擇的項",
      },
      us: {
        root: "Multiple root nodes",
        title: "Setup Function",
        selected: "Selected items:",
      },
    });
    const selected = ref("zh-cn");
    const selectedValue = computed(() => {
      const langs = data.languages.find((l) => l.key === selected.value);
      if (langs) {
        return langs.value;
      }
      return selected.value;
    });

    const selectLang = (key: string): void => {
      selected.value = key;
    };

    return {
      data,
      lang,
      selected,
      selectLang,
      selectedValue,
    };
  },
};
</script>
<style scoped></style>
