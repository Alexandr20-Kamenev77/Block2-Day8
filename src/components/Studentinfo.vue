<template>
  <div class="student-profile">
    <div class="student-info">
      <h2>{{ student.name }}</h2>
      <img :src="student.photo" :alt="student.name" class="student-photo">
    </div>
    <div class="student-details">
      <p><strong>Група:</strong> {{ student.group }}</p>
      <p><strong>Оцінка:</strong> {{ student.mark }}</p>
      <p><strong>Практика:</strong> {{ student.isDonePr ? 'Завершена' : 'Не завершена' }}</p>
      <p><strong>Кількість студентів:</strong> {{ studentCount }}</p>
    </div>
  </div>
</template>
<script>
import { ref, computed, onMounted } from 'vue';
import { useStore } from 'vuex';
export default {
  props: {
    id: String,
  },
  setup(props) {
    const store = useStore();
    const student = ref({});
    onMounted(async () => {
      try {
        const response = await fetchStudentData(props.id);
        student.value = response;
      } catch (error) {
        handleLoadError(error);
      }
    });
    const studentCount = computed(() => store.state.studentCount);
    return {
      student,
      studentCount,
    };
  },
};
async function fetchStudentData(id) {
  const apiUrl = `http://34.82.81.113:3000/students/${id}`;
  const response = await axios.get(apiUrl);
  return response.data;
}
function handleLoadError(error) {
  console.error("Помилка при завантаженні студента:", error);
}
</script>