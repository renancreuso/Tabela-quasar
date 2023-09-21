<template>
  <q-page>
    <div class="row">
      <!-- separator="cell"  na q-table para mudar o estilo da tabela -->
      <q-table
        dense
        title="Tabela"
        :rows="rows"
        :columns="columns"
        row-key="id"
        class="col"
      >
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
      </q-table>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  data() {
    return {
      columns: [
        {
          name: "id",
          label: "Post",
          align: "left",
          field: "id",
          sortable: true,
          class: " col-sm-3",
        },
        {
          name: "title",
          label: "Name",
          align: "left",
          field: "title",
          sortable: true,
        },
        {
          name: "action",
          label: "",
          align: "right",
        },
      ],

      rows: [],
    };
  },
  mounted() {
    this.getPosts();
  },
  methods: {
    getPosts() {
      this.$axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then((res) => {
          this.rows = res.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    editPost(idPost) {
      const index = this.rows.findIndex((item) => item.id === idPost);

      if (index !== -1) {
        const editedItem = this.rows[index];

        editedItem.title = "Novo Título"; // Substitua "Novo Título" pelo novo título desejado

        this.rows.splice(index, 1, editedItem); // Atualize a matriz com o item editado

        console.log("linha editada: ", idPost);
      }
    },

    deletePost(idPost) {
      const index = this.rows.findIndex((item) => {
        item.id === idPost;
      });
      if (index !== -1) {
        this.rows.splice(index, 1);
      }

      console.log("linha deletada", idPost);
    },
  },
});
</script>
