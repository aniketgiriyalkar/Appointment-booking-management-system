<template>
  <div id="main-app" class="container">
    <div class="row justify-content-center">
      <add-appointment @add="addItem" />
      <search-appointments
        @searchRecords="searchAppointments"
        :myKey="filterKey"
        :myDir="filterDir"
        @request-key="changeKey"
        @request-dir="changeDir"
      /> 
      <appointment-list :appointments="filteredApts" @remove="removeItem" @edit="editItem" />
    </div>
    
  </div>
</template>

<script>
import AppointmentList from "./components/AppointmentList";
import AddAppointment from "./components/AddAppointment";
import SearchAppointments from "./components/SearchAppointments";
import axios from "axios";
import _ from "lodash";

export default {
  name: 'MainApp',
  data: function() {
    return  {
      appointments: [],
      filterKey: "petName",
      filterDir: "asc",
      searchTerms: "",
      aptIndex: 0
    };
  },
  computed: {
    searchedApts: function() {
      return this.appointments.filter(item => {
        return(
          item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase()) 
        );
      });
    },
    filteredApts: function () {
      return _.orderBy(
        this.searchedApts,
        item => {
          return item[this.filterKey].toLowerCase();
        }, this.filterDir
      );
    }
  },
  components: {
    AppointmentList,
    AddAppointment,
    SearchAppointments
  },
  methods: {
    searchAppointments: function (terms) {
      this.searchTerms = terms;
    },
    addItem: function(apt) {
      apt.aptId = this.aptIndex;
      this.aptIndex++;
      this.appointments.push(apt);
    },
    removeItem: function(apt) {
      this.appointments = _.without(this.appointments, apt);
    },
    editItem: function(id, field, text) {
      const aptIndex = _.findIndex(this.appointments, {
        aptId: id
      });
      this.appointments[aptIndex][field] = text;
    },
    changeKey: function(value) {
      this.filterKey = value;
    },
    changeDir: function(value) {
      this.filterDir = value;
    }
  },
  mounted() {
    axios.get("./data/appointments.json")
    .then(response => (this.appointments = response.data.map(item => {
      item.aptId = this.aptIndex;
      this.aptIndex++;
      return item
    })));
  }
}
</script>
