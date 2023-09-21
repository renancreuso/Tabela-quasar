<template v-slot:body-cell-action="props">
  <q-td :props="props">
    <div>
      <q-btn
        icon="create"
        size="sm"
        color="primary"
        dense
        @click="editPost(props.row.id)"
      />
      <q-btn
        icon="delete"
        size="sm"
        color="negative"
        dense
        class="q-ml-sm"
        @click="deletePost(props.row.id)"
      />
    </div>
  </q-td>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "ColunaBotao",

  props: {
    row: Object, // Receba props como um objeto
  },
});
</script>
