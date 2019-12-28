<template>
  <div id="app">
    <Toast :message="toast.message" :context="toast.context" v-if="toast.show" />
    <header>
      <div>{{projectsData.total}} Projects</div>
      <div class="pagination">
        {{projectsData.from}}-{{projectsData.to}} of {{projectsData.total}}
        <svg
          aria-hidden="true"
          data-icon="caret-right"
          class="caret-right"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 192 512"
        >
          <path
            fill="currentColor"
            d="M0 384.662V127.338c0-17.818 21.543-26.741 34.142-14.142l128.662 128.662c7.81 7.81 7.81 20.474 0 28.284L34.142 398.804C21.543 411.404 0 402.48 0 384.662z"
          />
        </svg>
      </div>
      <div>
        <ToggleButton />
      </div>
    </header>

    <main>
      <table>
        <thead>
          <tr>
            <th>Project Name</th>
            <th>Developer</th>
            <th>Main Contractor</th>
            <th>Area</th>
            <th>State</th>
            <th class="status-head">
              <span>Status</span>
              <svg
                aria-hidden="true"
                data-icon="caret-down"
                class="caret-down"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 320 512"
              >
                <path
                  fill="currentColor"
                  class="caret"
                  d="M31.3 192h257.3c17.8 0 26.7 21.5 14.1 34.1L174.1 354.8c-7.8 7.8-20.5 7.8-28.3 0L17.2 226.1C4.6 213.5 13.5 192 31.3 192z"
                />
              </svg>
            </th>
            <th>Sector</th>
          </tr>
        </thead>
        <tbody>
          <tr
            :class="[showByIndex === index && hover == true ? 'blur': ' ' ]"
            v-for="(project, index) in projects"
            :key="index"
            @mouseover="hover = true, showByIndex = index"
            @mouseleave="hover = false"
          >
            <td>{{project.project_name}}</td>
            <td>{{project.developer}}</td>
            <td>{{project.main_contractor}}</td>
            <td>{{project.lga}}</td>
            <td>{{project.region}}</td>
            <td class="status-container">
              <span class="status">{{project.status}}</span>
            </td>
            <td>{{project.sector}}</td>
            <ViewMore v-show="showByIndex === index" :hover="hover" />
          </tr>
        </tbody>
      </table>
    </main>
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
      },
      hover: false,
      showByIndex: null,
      projectsData: {
        current_page: null,
        from: null,
        last_page: null,
        path: null,
        per_page: null,
        to: null,
        total: null
      }
    };
  },
  components: {
    Toast: () => import("@/components/Toast"),
    ViewMore: () => import("@/components/ViewMoreButton"),
    ToggleButton: () => import("@/components/ToggleButton")
  },
  methods: {
    getData: function() {
      axios
        .get("https://70c5b72c-65db-4a66-ba01-3e14763157e8.mock.pstmn.io/")
        .then(response => {
          this.projects = response.data.data;
          this.projectsData = { ...response.data.meta };
        })
        .catch(error => this.showToast(error, "error"));
    },
    showToast: function(message, context) {
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
  margin: 0 !important;
}
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #f6fafd;
  font-family: "Roboto";
  padding: 5rem 0;
}
header {
  width: 100%;
  display: flex;
  justify-content: space-around;
  margin-top: 5rem;
  margin-bottom: 1rem;
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
  }
  .status-head {
    display: flex;
    justify-content: space-around;
  }
}
.caret-down,
.caret-right {
  height: 1rem;
  width: 0.6rem;
}
.caret-right {
  margin-top: 0.3rem;
  margin-left: 2rem;
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
    padding: 1.5rem 0.6rem;
    text-align: start;
    &:first-child {
      border-right: solid 2px #c4c4c4;
      &:hover {
        cursor: pointer;
      }
    }
  }
  .status {
    background: #fadaa1;
    color: #b9995f;
    padding: 0.2rem 0.3rem;
    font-size: 0.7rem;
  }
  .status-container {
    padding: 0;
  }
}
.blur {
  :nth-child(n + 2) {
    filter: blur(0.2rem);
  }
}
@media (max-width: 767px) {
  #app {
    display: table;
    height: 100%;
  }
  body {

    height: 100% !important;
  }
  table{
  height: 80%;
  }
  thead {
    th {
        white-space: nowrap;
        width: fit-content;
    }
  }
}
@media (min-width: 768px) and (max-width: 1024px) {
  #app {
    display: table;
    height: 100%;
  }
  th {
    width: fit-content;
  }
  thead {
    th {
      white-space: nowrap;
    }
  }

}
@media (min-width: 1025px) {
  #app {
    width: 100%;

  }
  body {
    width: 100%;
  }
  main {
    width: 90%;
  }
  thead {
    th {
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
      justify-content: space-around;
    }
  }
}
</style>
