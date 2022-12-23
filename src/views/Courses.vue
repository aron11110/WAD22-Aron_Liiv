<template>
<div>
<h3> Courses  </h3>
<table>
          <tr>
            <th>Code</th>
            <th>Title</th>
            <th>Semester</th>
            <th>Credits</th>
            <th>Description</th>
          </tr>
          <tr class="courses" v-for="course in courses" :key="course.id">
            <td>{{course.code}}</td>
            <td>{{course.title}}</td>
            <td v-if="course.semester === 'spring'"><router-link to="/semester/spring">{{course.semester}}</router-link></td>
            <td v-else-if="course.semester === 'fall'"><router-link to="/semester/fall">{{course.semester}}</router-link></td>
            <td>{{course.credits}}</td>
            <td v-if="course.description === ''">No course description is provided</td>
            <td v-else>{{course.description}}</td>

          </tr>


</table> 
</div>
</template>

<script>
export default {
  name: "Courses",
  data() {
    return {
      courses: [],
    };
  },
  methods: {
    fetchCourses() {
      fetch(`http://localhost:3000/api/courses/`)
        .then((response) => response.json())
        .then((data) => (this.courses = data))
        .catch((err) => console.log(err.message));
   },
  },
  mounted() {
    this.fetchCourses();
    console.log("mounted");
  } 
};
</script>

<style scoped>
th {
  background: rgb(0, 131, 33);
  padding: 10px;
}
td {
  background: rgb(56, 163, 83);
  padding: 10px;
}
table {
  margin-left: 7%;
  margin-right: 7%;
}

</style>