<template>
  <router-link to="/add">Add New +</router-link>

  <table v-if="userDataArr && userDataArr.length">
    <tr>
      <th>First name</th>
      <th>Last name</th>
      <th>Phone number</th>
      <th>Designation</th>
      <th>Email</th>
      <th>State</th>
      <th>City</th>
      <th>Gender</th>
      <th>Date of birth</th>
      <th>Relationship status</th>
      <th>Action</th>
    </tr>
    <tr v-for="(data, index) in userDataArr" :key="index">
      <td>{{ data.firstName }}</td>
      <td>{{ data.lastName }}</td>
      <td>{{ data.phoneNumber }}</td>
      <td>{{ data.designation }}</td>
      <td>{{ data.email }}</td>
      <td>{{ data.state }}</td>
      <td>{{ data.city }}</td>
      <td>{{ data.gender }}</td>
      <td>{{ data.date }}</td>
      <td>{{ data.relationship }}</td>
      <td>
        <button class="edit" @click="editRow(data._id)" type="button">
          Edit
        </button>

        <button class="delete" @click="deleteRow(data._id)" type="button">
          Delete
        </button>
      </td>
    </tr>
  </table>
  <div v-else>No data is available</div>
</template>

<script>
import { ref } from "vue";
import { useRouter } from "vue-router";
export default {
  name: "UserDataList",
  setup() {
    const data = ref(null);
    const router = useRouter();
    const userDataArr = ref(
      JSON.parse(window.localStorage.getItem("submitValue"))
    );

    const editRow = (id) => {
      console.log("edit", id);
      router.push({ name: "update", params: { uid: id } });
    };
    const deleteRow = (id) => {
      userDataArr.value = userDataArr.value.filter((el) => el._id !== id);

      window.localStorage.setItem(
        "submitValue",
        JSON.stringify(userDataArr.value)
      );
    };

    return {
      data,
      editRow,
      deleteRow,
      userDataArr,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
table {
  margin-top: 20px;
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  border-radius: 4px;
  background-color: #199319;
  color: white;
  padding: 8px 8px;
  text-decoration: none;
}
button {
  width: 4rem;
  height: 2rem;
  border: none;
  font-size: 100%;
  padding: 7px 7px;
  color: white;
  border-radius: 4px;
  cursor: pointer;
  &.edit {
    background-color: #224494;
    margin-right: 10%;
  }
  &.delete {
    background-color: #931921;
  }
}
</style>
