<template>
  <div id="app">
    <Toast />
    <main>
      <table>
        <thead>
          <tr>
            <th>Project Name</th>
            <th>Developer</th>
            <th>Main Contractor</th>
            <th>Area</th>
            <th>State</th>
            <th class="status-head"> <span> Status </span> <svg aria-hidden="true" data-prefix="fas" data-icon="caret-down" class="caret-down" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512"><path fill="currentColor" class="caret" d="M31.3 192h257.3c17.8 0 26.7 21.5 14.1 34.1L174.1 354.8c-7.8 7.8-20.5 7.8-28.3 0L17.2 226.1C4.6 213.5 13.5 192 31.3 192z"/></svg></th>
            <th>Sector</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="project in projects" :key="project.id">
            <td>{{project.project_name}}</td>
            <td>{{project.developer}}</td>
            <td>{{project.main_contractor}}</td>
            <td>{{project.lga}}</td>
            <td>{{project.region}}</td>
            <td class="status-container">
              <span class="status">{{project.status}}</span>
            </td>
            <td>{{project.sector}}</td>
          </tr>
        </tbody>
      </table>
    </main>
    <ViewMore />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      projects: [],
      toast: {
        message: "",
        context: "",
        show: false
      }
    };
  },
  components: {
    Toast: () => import("@/components/Toast"),
    ViewMore: () => import("@/components/ViewMoreButton")
  },
  methods: {
    getData: function() {
      axios
        .get("https://70c5b72c-65db-4a66-ba01-3e14763157e8.mock.pstmn.io/")
        .then(response => {
          this.projects = response.data.data;
          console.log(this.projects);
          // this.showToast(,'error'));
          // document.write(response.data)
        })
        .catch(error => this.showToast(error, "error"));
    },
    showToast: function({ message, context }) {
      this.toast = { message, context, show: true };
      setTimeout(() => {
        this.toast = { message: " ", context: " ", show: false };
      }, 3000);
    }
  },
  mounted() {
    this.getData();
  },
  computed: {}
};
</script>

<style lang="scss" >
body {
  width: 100%;
  overflow-y: hidden;
  margin: 0 !important;
}
#app {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #f6fafd;
  font-family: "Roboto";
  /* padding: 2rem; */
}
table,
th,
td {
  border-collapse: collapse;
  border-spacing: 0;
}
main {
  display: flex;
  justify-content: center;
  width: 90%;
}
table {
  width: 100%;
  border: 1px solid #f6fafd;
  box-shadow: 5px 2px 5px 2px #edf4fc;
  letter-spacing: 0.3px;
  margin-bottom: 2rem;
}
thead {
  width: 100%;
  color: #fff;
  background-color: #2a3a49;
 

  th {
    padding: 1rem 0.5rem;
    text-align: start;
    font-size: 0.8rem;
    &:nth-child(1) {
      width: 18%;
    }
    &:nth-child(2) {
      width: 18%;
    }
    &:nth-child(3) {
      width: 18%;
    }
  }
  .status-head {
      display: flex;
      justify-content: space-around
  }
  .caret-down{
    height: 1rem;
    width: .6rem;

 
  }
}
tbody {
  background: #fff;
  tr {
    &:nth-child(odd) {
      background-color: #f6fafd;
    }
  }
  td {
    font-size: 0.8rem;
    padding: 1rem 0.6rem;
    text-align: start;
    &:first-child {
      border-right: solid 2px #c4c4c4;
    }
  }
  .status {
    background: #fadaa1;
    color: #b9995f;
    padding: 0.2rem 0.3rem;
    font-size: 0.7rem;
    /* margin:0 .5rem */
  }
  .status-container {
    padding: 0;
    /* text-align: center; */
  }
}
</style>
