<template>
  <app-page title="Список заявок">
    <template #header>
      <button class="btn primary" @click="modal = true">Создать</button>
    </template>

    <request-table :request="requests"></request-table>

    <teleport to="body">
      <app-modal v-if="modal" title="Создать заявку" @close="modal = false">
        <request-modal @created="modal = false" />
      </app-modal>
    </teleport>
  </app-page>
</template>

<script>
import {ref, computed} from 'vue';
import {useStore} from "vuex";
import AppPage from "@/components/ui/AppPage";
import RequestTable from "@/components/request/RequestTable";
import RequestModal from "@/components/request/RequestModal";
import AppModal from "@/components/ui/AppModal";

export default {
  setup() {
    const store = useStore();
    const modal = ref(false);

    const requests = computed(() => store.getters['request/requests'])

    return {
      modal,
      requests,
    }
  },
  components: {
    AppPage,
    RequestTable,
    AppModal,
    RequestModal,
  }
}
</script>
