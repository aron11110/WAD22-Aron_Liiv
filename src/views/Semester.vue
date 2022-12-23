<template>
<div>
    <h3 v-if="$route.params.id === 'fall'"> fall  </h3>
    <h3 v-else-if="'spring'"> spring </h3>
          <div v-if="$route.params.id === 'fall'">
        <table>
          <tr>
            <th>Code</th>
            <th>Title</th>
            <th>Semester</th>
            <th>Credits</th>
            <th>Description</th>
          </tr>

            <tr class="courses"  v-for="course in Fall" :key="course.id">
            <td>{{course.code}}</td>
            <td>{{course.title}}</td>
            <td>{{course.semester}}</td>
            <td>{{course.credits}}</td>
            <td v-if="course.description === ''">No course description is provided</td>
            <td v-else>{{course.description}}</td>

          </tr>
          </table>
          </div>
          <div v-else-if="'spring'">
            <table>
            <tr>
                <th>Code</th>
                <th>Title</th>
                <th>Semester</th>
                <th>Credits</th>
                <th>Description</th>
            </tr>

            <tr class="courses"  v-for="course in Spring" :key="course.id">
            <td>{{course.code}}</td>
            <td>{{course.title}}</td>
            <td>{{course.semester}}</td>
            <td>{{course.credits}}</td>
            <td v-if="course.description === ''">No course description is provided</td>
            <td v-else>{{course.description}}</td>
          </tr>
          </table>


          </div>
          


</div>
<a href="/courses"> Back to courses </a>
</template>


<script>
export default {
    name: "Semester",
    data() {
        return {
            Fall: [],
            Spring: []
        }
    },
    methods: {
        // fetch_courses() {
        //     fetch(`http://localhost:3000/api/courses/`)
        //     .then((response) => response.json())
        //     .then((res) => {
        //         for (let i = 0; i < res.length; i++) {
        //             console.log(res[i])
        //             if (res[i].semester === "spring") {
        //                 this.Spring.push(res[i])
        //             } else {
        //                 this.Fall.push(res[i])
        //             }
        //         }
        //     })
        // }
        fetch_spring() {
            fetch('http://localhost:3000/api/semesters/spring')
            .then((response) => response.json())
            .then((data) => this.Spring = data)
            .then(console.log(this.Spring))
        },
        fetch_fall() {
            fetch('http://localhost:3000/api/semesters/fall')
            .then((response) => response.json())
            .then((data) => this.Fall = data)
            .then(console.log(this.Fall))

        }

    },
    mounted() {
        if (this.$route.params.id === 'spring') {
            this.fetch_spring()
        } else if (this.$route.params.id === 'fall') {
            this.fetch_fall()
        }
    }

}
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