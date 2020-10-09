# Appointment-booking-management
- Aniket Giriyalkar (giriyalkar.aniket@gmail.com)
- In this project, I build a component based application: Appointment Booking and Management System with features of searching and sorting.
- The end goal is a functional app prototype and more skills with this flexible framework. We learn to use Vue.js components and subcomponents; build forms; create, update and delete data and manage events.

## Installations

- Official tool for building applications with Vue.js is Vue CLI. CLI stands for command line interface. Make sure node is installed before installing the Vue CLI. Then use the following command in the command line to install the CLI:
```np
npm install -g @vue/cli
```

- Then go into the project directory by doing a cd, for me its Desktop\Appointment-Booking-Mgmt\Appointment-booking-management-system and type the following: 
```
vue create appointment-booking-mgmt
```
appointment-booking-mgmt is the name of the our project.

- We go ahead with an option of picking the default settings( version 2.x of Vue.js ) for the installation

- Once the installation is done, cd into the project directory(cd .\appointment-booking-mgmt) and type the command
```
npm run serve
```
- This will start running the development version of the server and is going to process the project. App runs at http://localhost:8081 in the browser.

### Understanding Vue CLI installations
- It is important to know what is going on when you install things on the terminal.The application hads a readme file that has a list of commands one can run. We have already used npm run serve command. "npm run build" command will build the development version of your application. This is going to make another directory in there and what's in that directory is what we will be uploading on the server.
- Since, this is a typical node package manager we will have a package.json file which will have a list of all the dependencies and developer dependencies, as well as some additional configuration that you can use. When we run the npm run serve or npm run build commands, we are actually using a module called VUE CLI service. Dependencies are the extensions or the modules that get installed by the command line interface. These go into the node modules foder. @vue is a folder in there where most of these commands are coming from. 
- .gitignore just allows you to control which sort of folders are tracked by git. The dist folder which is the folder that gets created when you run an npm run build command is called and this tells git not to upload this folder to GitHub or wherever you're managing your code. In addition to that, we have a couple of other folders, the public as well as the src folder. The public folder is where you put anything that you want to be accessible on the web after this application is processed. So if you want to you can include images in here. And we have this thing called a favicon, this little V right now, which you can see usually at the top of your browsers, right over here.
- We have the index.html file where there is an assests folder which currently has the logo. This is sort of where we would put things that we want our Vue application to know about and control. And then all the stuff in the src folder will get processed and placed somewhere. So that either the live reload server that is running will display it or when you run the npm build command so that that folder that gets created with all of the output files has everything they need.
- We have a main.js which is the first file that gets loaded by vue.js. We are loading out the Vue library as well as a component here. This si the master/ root component. We are asking vue to render everything with ID of app.
- In the index.html, there's a div which has the id app. From here we call the sub-component called app.vue. Eveything else happens in the component here.
- In each component file we create three different sections, a template section, a script section and a style section. The style section is optional. In the template section, we put in the html.
- We can load some things into the index.html file. But it's sort of nice to have everything that's required for a component within the component itself. This will also prevent styles that appear here only apply to the component that we are in, and not to other parent components.

### Installing custom modules
Bootstap jquery(bootstrap dependency) popper.js are some modules we will be installing. This can be done in a single statement:
```
npm i --save bootstrap jquery popper.js
```
Then we install the libraries lodash moment and axios using the following command:
```
npm i --save lodash moment axios
```

Next, we install a font library called font awesome using the follwoing command: 
```
npm i --save @fortawesome/fontawesome-free @fortawesome/fontawesome-svg-core @fortawesome/free-solid-svg-icons @fortawesome/vue-fontawesome
```

- All these got added as dependencies in our package.json file.

## Working with Modules and Data

### Cleaning up and loading a module
- Next we get rid of all the unnecessary files that we won't be using. We remove the assets folder for now and also the components folder as we are not using it. We also remove the HelloWorld.vue and assets reference from the App.vue file.
- To test if the App is still running properly we enter something in the div to see if it shows up on execution.
- Next, we see how to bring data into the component. We can put in a data attribute in this configuration object. The way that Vue.js works is by giving you this configuration object. The data element works is in a couple of different ways, if you're using script based Vue then you could just create an object in there, and add name and value pairs and pass along data directly. If we are using components then we have to do it a little bit differently, this needs to be a function and that function needs to return something. We will create a title field, and type in Appointment List and then we can use message interpolation to output that title. This is a basic way to get something printed out in Vue.js.
- The nomenclature of class name and component name is a bit confusing. We change the div id name to "main-app" and the component name to MainApp. We see to it that changing the names does not affect any thing with respect to the working of app.

- In the main.js file, we import bootstrap and the bootstrap css folder manually so that it is available to all the components. 
```
import "bootstrap";
import "bootstrap/dist/css/bootstrap.css";
```
- As soon as we save the file, we see that the text styling is now in the form of bootstrap.
- When we go to the App.vue and add class="container" in the div and save the file. We should see that our application is now responsive and adheres to the Bootstrap breakpoints.

### Importing Font Awesome Library
-  In the main.js we import the library component from the Font Awesome module.
```
import { library } from "@fortawesome/fontawesome-svg-core";
```

- Then we import selective icons that we would be needing and add them to the library that we imported above
```
import {
  faPlus, faMinus, faTrash, faCheck
} from "@fortawesome/free-solid-svg-icons";

library.add(faPlus, faMinus, faTrash, faCheck);
```
- Then to check if the imports are working correctly, in the App.vue file, in the beginning of the script tag, we import the FontAwesomeIcon.
- Before we use these icons in the template, we need to make sure that these are included in the components that we include.
```
<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

export default {
  name: 'MainApp',
  data: function() {
    return  {
      title: "Appointment List"
    };
  },
  components: {
    FontAwesomeIcon
  }
}
</script>
```
- Then in the template we can call the font-awesone-icon component and view the plus icon by the following statement:
```
<template>
  <div id="main-app" class="container">
    <h4>{{ title }}</h4>
    <font-awesome-icon icon="plus" class="mr-2"/> Add appointment
  </div>
</template>
```
### Looping through the data
- From the Github Url: https://gist.githubusercontent.com/planetoftheweb/46426d47f21f2c9245bbe23f0fb834b5/raw/afae0adf97472893288ac5cde69e7bbb770793ed/appointments.json, we get the sample data that we will require for our project. We add this array of objects to the data section as the value to the appointments key in App.vue.
- Next task is to display all this data into the template tag and hence the browser. For that we create a template where we can pass the data easily.
- Since there are multiple appointment data, it makes sense to loop through each appointment data. we use the v-for directive.
```
<template>
  <div id="main-app" class="container">
    <h4>{{ title }}</h4>
    <font-awesome-icon icon="plus" class="mr-2"/> Add appointment
    <div v-for="(item, index) in appointments" v-bind:key="index">
      <h4>{{ item.petName }}</h4>
      <p>{{ item.aptNotes }}</p>
    </div>
  </div>
</template>

<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

export default {
  name: 'MainApp',
  data: function() {
    return  {
      title: "Appointment List",
      appointments: [
        {
          "petName":"Spot",
          "petOwner":"Constance Smith",
          "aptDate":"2017-07-24 08:30",
          "aptNotes":"This German Shepherd is having some back pain"
        },
        {
          "petName":"Goldie",
          "petOwner":"Barot Bellingham",
          "aptDate":"2017-07-22 15:50",
          "aptNotes":"This Goldfish has some weird spots in the belly"
        },
        {
          "petName":"Mitten",
          "petOwner":"Hillary Goldwyn",
          "aptDate":"2017-07-21 9:15",
          "aptNotes":"Cat has excessive hairballs"
        },
        {
          "petName":"Buffy",
          "petOwner":"Hassum Harrod",
          "aptDate":"2017-07-20 15:30",
          "aptNotes":"This Chihuahua has not eaten for three days and is lethargic"
        }
      ]
    };
  },
  components: {
    FontAwesomeIcon
  }
}
</script>
```

### Using axios to import data
- We installed Axios, which is a promise based Http client and provides a very compatible way of performing AJAX cells. It is more compatible than the fetch API in javascript.
- Now we remove all the appoints from the data in the App.js and move it to data/appointments.json (create a folder and the file and cutn paste the information there). 
- In the App.vue, we import the axios from axios library and then add a lifecycle hook called mounted method to the App.vue. This method is called in the start of the application and hence is a great place to load files or load data into.
- We will call the axios library and use the "get" method. Then we will locate that data folder and appointments.json and then we will call a promise. We will receive a response from the promise and based on that response we set the value of the appointments variable to our response data.
- So the response is an HTTP like response that just has all kinds of information,  we will be using the data property of that response, which will work pretty well, and axios is just going to sort of make the process of getting the data a lot easier.
- The fetch API is also pretty easy and it is also promise based, but again axios makes it a little more compatible with older browsers.
```
<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import axios from "axios";

export default {
  name: 'MainApp',
  data: function() {
    return  {
      title: "Appointment List",
      appointments: []
    };
  },
  components: {
    FontAwesomeIcon
  },
  mounted() {
    axios.get("./data/appointments.json")
    .then(response => (this.appointments = response.data));
  }
}
</script>
```
- Now we save and observe that everything is working fine. and the data is accurately showing up on the screen.

## Props, Methods and Events

### Using props in subcomponents
- Lets create a seperate component that creats a list to place the elements. It is common to create subcomponents so that we can reuse the things and also make the code a little cleaner and shorter in different places.
- We will create a new folder in the src directory called the components. Then we create a file called AppointmentList.vue. In here we create different sections in a view as component. The template that consists of a single container div which will have the code to display each pet name and appointment notes.
- Next, we create a script section in which we give the name of this component as AppointmentList. Then we need to pass the appointment information to this component which we are going to do through something called props.
- We will have to specify that the props that this component needs is going to be appointments.
- To make this component work we need to go back to App.vue and add our newly created component to the components call. For that in the App.vue we import the AppointmentList in here and add that to the components list.
- Next, we call the appointment-list component within the div in the template. We include a v-bind directive to be able to pass along the appointments information(which will have the same name as the name of the variable in the subcomponent). 
```
 <appointment-list :appointments="appointments"/>
```
- :appointments is a shorthand notation for vbind:appointments="appointments". On the right side of the = sign is the information from the App.vue file that we wish to pass to our component. It may seem like a html tag but we are passing the real varirables containing information inside the "".

- Now we add some bootstrap classes for better visualization into our AppointmentList.vue component. Since we are not using FontAwesomeIcon in the App.vue anymore we remove it from there and import it into AppointmentList component and use the trash icon which will look visually attractive. Here is what the component looks like:
```
<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="list-group list-group-flush">
      <div 
        class="list-group-item d-flex align-items-start"
        v-for="(item, index) in appointments"
        v-bind:key="index"
      >
        <button class="mr-2 btn btn-sm btn-danger">
          <font-awesome-icon icon="trash" />
        </button>
        <div class="w-100">
          <div class="d-flex justify-content-between">
            <span class="h4 text-primary">{{item.petName}}</span>
            <span class="float-right">{{item.aptDate}}</span>
          </div>
          <div class="owner-name">
            <span class="font-weight-bold text-primary mr-1">Owner:</span>
            <span>{{item.petOwner}}</span>
          </div>
          <div>{{item.aptNotes}}</div>
        </div>
      </div>
    </div>
  </div>  
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  name: "AppointmentList",
  components: {
    FontAwesomeIcon
  },
  props: ["appointments"]
    
};
</script>
```
- In the App.vue, we embedd the appointmentlist component inside a div so that the bootstrap styling applies as expected and makes it responsive.  
```
<template>
  <div id="main-app" class="container">
    <div class="row justify-content-center">
      <appointment-list :appointments="appointments"/>
    </div>
    
  </div>
</template>
```

### Using Moment.js for dates
- Currently the dates are visible in an ordinary military format. We can use a library called Moment.js (https://momentjs.com) from javascript to improve the representation of date and time.
- In AppointmentList.vue, we import Moment from Moment library. We create a method, which are sort of like functions in Vue.js and we can call them from within our template and they will execute, return or transform something within the applicaiton.
- We are going to create a formatted date function, that receives a date as parameter and return a date that is formatted in the form of "MM-DD-YY, h:mm a"
```
<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import moment from "moment";

export default {
  name: "AppointmentList",
  components: {
    FontAwesomeIcon
  },
  methods: {
    formattedDate: function(date) {
      return moment(new Date(date)).format("MM-DD-YY, h:mm a");
    }  
  },
  props: ["appointments"]
    
};
</script>
```
- Then inside the template, instead of outputting somthing from the item, we will use our method to display the date.
```
  <span class="float-right">{{formattedDate(item.aptDate)}}</span>
```
- We see that the dates no appear in the formatted manner. Moment is hence very easy to work with as we just saw.

### Deleting records using events
- Now we need to wire up the functionality of Delete buttons. To do this, we make use of events.
- To create an even in Vue.js we use @ followed by the name of the event we want to trigger. In our case we have the event @click and assign it to a method that we will be creating. But the data that we want to use does not exist in this component, it exists in the parent component. This scenario is quite common in Vue.js. Generally, we leave all our data in the main component and tell our sub-components to do something on the main component.
- So in case of the sub-event, instead of calling a local method, we issue an emit event and this will generate an event on the parent component. The event we want is going to be called remove and we pass along the item we want to remove. In our cae, the item is going to be the element that we will be looping through.
- In the App.vue, we will have to wire this up. We will have to inform the appointment-list component about the "remove" event we are looking for to take place. And when it happens we will call a local method called "removeItem". We will have to create the removeItem method in the methods section. Item parameter which we are passing from the subcomponent will be automatically passed. We do not have to specify it in the parent component.
- Now we capture that appointment and reset the appointment erase so that it no longer has it. We can write an array element removal function but to simplify things, we use the lodash library. We import the lodash library and use the without method from it.
```
methods: {
    removeItem: function(apt) {
      this.appointments = _.without(this.appointments, apt);
    }
  }  
```
- Lodash without call allows you to specify an element and it is going to look through an array which we are passing and return a new array that dosen't have the specified element in it.
- Now when we save and go on to look at the items. We see that on pressing the trash icon they are automatically deleted.

## Indexing, Editing and Adding Records
### Creating an Index
- Index is important to uniquely identify each appointment. If the same appointment list is sorted the placemnet would differ and deleting elements will affect the indexes. To take care of these issues we will add index so that every element will have a uniqueId. 
- We do this by using map javascript function. We update the data and mounted fields in the App.vue file. 
```
data: function() {
    return  {
      appointments: [],
      aptIndex: 0
    };
  },
 mounted() {
    axios.get("./data/appointments.json")
    .then(response => (this.appointments = response.data.map(item => {
      item.aptId = this.aptIndex;
      this.aptIndex++;
      return item
    })));
  }
``` 
- Now that we can identify each item individually, in the AppointmentList.vue 
```
  <div 
    class="list-group-item d-flex align-items-start"
    v-for="(item, index) in appointments"
    v-bind:key="index"
  >
```
There is no longer a need for index, we can use aptIndex like:
```
  <div 
    class="list-group-item d-flex align-items-start"
    v-for="item in appointments"
    v-bind:key="item.aptIndex"
  >
```
- When we use the Vue.js chrome developer tool, we can see that an apt.Id exists for all the elements.

### Editing existing items
- Now to allow the users to modify these fields, we will be using something in HTML called Content Editable, which will let us modify some of these HTML element. 
- In the span that contains the petName we add :
```
  <span
    class="h4 text-primary"
    contenteditable="contenteditable"
    @blur="$emit('edit', item.aptId, 'petName', $event.target.innerText)"
  >{{item.petName}}</span>
```  
where contenteditable will have the value contenteditable. We look for a blur event that happens when somebody modifies one of the contenteditable fields. We will emit this event, it will send to the parent component an event we will be calling edit.
- Along with this we will pass the item.aptId which is the index that we created. We also pass the name of the field we want to modify, which is petName in this case, so we will pass that along. Ans we will need to pass the infromation about the element that was changed.
- When we click on one of these elements, the element itself has an item called innerHTML we can look for that text as it gets modified, we are going to look for the event information. Vue.js keeps track of this information.
- We do the same for the Pet Owner and Appointment Notes fields
```
  <span
    contenteditable="contenteditable"
    @blur="$emit('edit', item.aptId, 'petOwner', $event.target.innerText)"
  >{{item.petOwner}}</span>
  <div
    contenteditable="contenteditable"
    @blur="$emit('edit', item.aptId, 'aptNotes', $event.target.innerText)"
  >{{item.aptNotes}}</div>
```
- In the App.vue, we capture the event that took place. We call it @edit and assign the editItem function to it. Now we will have to create the method editItem.
```
editItem: function(id, field, text) {
      const aptIndex = _.findIndex(this.appointments, {
        aptId: id
      });
      this.appointments[aptIndex][field] = text;
    }
```
On saving and running the application we see that, we can edit the fields title, owner and appointment notes. We can verify that the changes are getting reflected at element level by inspecting with the help of Vue developer tools and observe that the changes are getting reflected.

### Adding new items
- We create a new component called AddAppointment.vue
```
<template>
  <div class="col-12">
    <div class="card textcenter mt-3">
      <div class="card-header bg-primary text-white">
        <font-awesome-icon icon="plus" class="mr-3"/>Add Appointment
      </div>

      <div class="card-body">
        <form id="aptForm">
          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="petName">Pet Name</label>
            <div class="col-md-10">
              <input
                type="text"
                class="form-control"
                name="petName"
                id="petName"
                placeholder="Pet's Name"
              >
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="ownerName">Pet Owner</label>
            <div class="col-md-10">
              <input type="text" class="form-control" id="ownerName" placeholder="Owner's Name">
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 col-form-label text-md-right" for="aptDate">Date</label>
            <div class="col-md-4">
              <input type="date" class="form-control" id="aptDate">
            </div>
            <label class="col-md-2 col-form-label text-md-right" for="aptTime">Time</label>
            <div class="col-md-4">
              <input type="time" class="form-control" name="aptTime" id="aptTime">
            </div>
          </div>

          <div class="form-group form-row">
            <label class="col-md-2 text-md-right" for="aptNotes">Apt. Notes</label>
            <div class="col-md-10">
              <textarea
                class="form-control"
                rows="4"
                cols="50"
                name="aptNotes"
                id="aptNotes"
                placeholder="Appointment Notes"
              ></textarea>
            </div>
          </div>

          <div class="form-group form-row mb-0">
            <div class="offset-md-2 col-md-10">
              <button type="submit" class="btn btn-primary d-block ml-auto">Add Appointment</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
export default {
  name: "AddAppointment",
  data () {
    return {};
  },
  components: {
    FontAwesomeIcon
  }
    
}
</script>
```
- In the App.vue component, we need to import this component and call it before the appointment list component. Now we see that the Add appointment form appears above the Appointment list in the page. We need to make this form visible only on button click and not always, for that we create a handler in AddAppointment.vue
```
<div class="card-header bg-primary text-white" @click="hidepanel=!hidepanel">
```
- This will endure a toggling effect. Next we need to pass the initial value for hidepanel which we pass inside the data.
```
<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
export default {
  name: "AddAppointment",
  data () {
    return {
        hidepanel: true
    };
  },
  components: {
    FontAwesomeIcon
  }
}
</script>
```
- Then we need to show or not show the remainder of the form based on the value of hidepanel which is done by adding a v-bind:class property to the div that contains the form.
```
  <div class="card-body" :class="{'d-none': hidepanel}">
```
- We save and see that the toggle effect is exactly working as expected. The form appears and disappears on clicking the Add Appointment toggle.

### Managing the form with V-model
- To see to it that the input being entered in the form is being reflected we add a formData variable which is an empty array initially. We take the information from the form and store it in here. To use that we use v-model in the input tag and store it in a variable which in our case is formData.
```
  <input
    type="text"
    class="form-control"
    name="petName"
    id="petName"
    placeholder="Pet's Name"
    v-model="formData.petName"
  >
```
So, whenever we enter something in the inpuut field it will be stored in the formData. We do the same for other input fields.
```
  <input type="text" class="form-control" id="ownerName" placeholder="Owner's Name" v-model="formData.ownerName">
  <input type="date" class="form-control" id="aptDate" v-model="formData.aptDate">
  <input type="time" class="form-control" name="aptTime" id="aptTime" v-model="formData.aptTime">
  <textarea
    class="form-control"
    rows="4"
    cols="50"
    name="aptNotes"
    id="aptNotes"
    placeholder="Appointment Notes"
    v-model="formData.aptNotes"
  ></textarea>
```
- Once the data entered in all the input fields is being stored in an array. Then we will have to look into what happens when someone submits the form. In the form element we issue an event submit.
```
<form id="aptForm" @submit.prevent="requestAdd">
```
@submit.prevent will prevent the page from reloading and thus prevent the default behaviour of submit which would automatically refresh the page. We need to add a definition for requestAdd function. 

```
  methods: {
    requestAdd: function() {
      this.formData  = {
          petName: this.formData.petName,
          ownerName: this.formData.ownerName,
          aptDate: this.formData.aptDate + ' ' + this.formData.aptTime,
          aptNotes: this.formData.aptNotes
      };
    }
  },
```
- Once we save this file. We will test that the data is getting stored in the array by using the developer tools. We can clearly see that on pressing the submit button we can see our input reflecting in their respective fields in the formData object.

### Adding the records to the data
- Now that we can see our input reflecting in formData object, the next step is to push this information into the array when the submit button is hit.
- We need to emit an event once the form is submitted. Then we reset the formdata and set the hidepanel to true. We add this logic inside the requestAdd method.
```
  methods: {
    requestAdd: function() {
      this.formData  = {
          petName: this.formData.petName,
          ownerName: this.formData.ownerName,
          aptDate: this.formData.aptDate + ' ' + this.formData.aptTime,
          aptNotes: this.formData.aptNotes
      };
      this.$emit("add", this.formData);
      this.formData = [];
      this.hidepanel = true;
    }
  },
```
- In the main component(App.vue), we add this event to the add-appointment component as that is where the event is coming from.
```
  <add-appointment @add="addItem" />
```
- We need to define the addItem function in our methods. This method will take in the index from the aptIndex variable we created and adjust that index for the next item. Then we push the data into the appointments array and we should be good. 
```
methods: {
    addItem: function(apt) {
      apt.aptId = this.aptIndex;
      this.aptIndex++;
      this.appointments.push(apt);
    }
  },
```
- On testing, we see that the appointment is getting added to the list and visible on the screen after submitting the form. The new element shows up and when we open up the add appointment form again, it is empty as expected. This means everything is working as per our expectations.

## Searching and Filtering

- Next we create a new component called SearchAppointments for searching the appointments. In the data we will have a searchTerm which will store the search query.
```
SearchAppointments.vue
<template>
    <div class="col-12 col-md-10 col-lg-7">
    <div class="input-group my-3">
      <input
        id="SearchApts"
        placeholder="Search"
        type="text"
        class="form-control"
        aria-label="Search Appointments"
      >

      <div class="input-group-append">
        <button
          type="button"
          class="btn btn-primary dropdown-toggle"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
        >
          Sort by
          <span class="caret"></span>
        </button>

        <div class="dropdown-menu dropdown-menu-right">
          <a href="#" class="dropdown-item d-flex justify-content-between" id="petName">
            Pet Name
            <font-awesome-icon icon="check"/>
          </a>

          <a class="dropdown-item d-flex justify-content-between" href="#" id="aptDate">
            Date
            <font-awesome-icon icon="check"/>
          </a>

          <a href="#" class="dropdown-item d-flex justify-content-between" id="ownerName">
            Owner
            <font-awesome-icon icon="check"/>
          </a>

          <div class="dropdown-divider" role="separator"></div>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="asc"
          >
            Asc
            <font-awesome-icon icon="check"/>
          </a>

          <a
            class="dropdown-item d-flex justify-content-between"
            href="#"
            id="desc"
          >
            Desc
            <font-awesome-icon icon="check"/>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

export default {
  name: "SearchAppointments",
  data () {
    return {
        searchTerm: ""
    };
  },
  components: {
      FontAwesomeIcon
  }
}
</script>
```

- In the App.vue file we import this component and call it in between the add-appointment and appointment-list component
```
  import SearchAppointments from "./components/SearchAppointments";
```
- We see that the Search bar appears in between the Add appointment and Lists components. Now we have to wire up the functions in the dropdown.

### Building Search Methods
- We use v-model to fill in the search term from the input, similar to what we did for add appointment. In addition, we will create a new section called watch, which will allow us to track a variable as it changes in the document. @blur is not used because we want to track it in realtime and not after that field has lost focus.

```
  <input
    id="SearchApts"
    placeholder="Search"
    type="text"
    class="form-control"
    aria-label="Search Appointments"
    v-model="searchTerm"
  >
  export default {
    name: "SearchAppointments",
    data () {
      return {
          searchTerm: ""
      };
    },
    watch: {
      searchTerm: function() {
          this.$emit("searchRecords", this.searchTerm);
      }
    },
  };
```
- When the event triggers, we pass that searchTerm to the parent component. We go back to App.vue and in the search-appointments component we capture the event @searchRecords
```
  <search-appointments @searchRecords="searchAppointments" />
```
- Now, we need to define the method, searchAppointments method and add the searchTerms in the data
```
  data: function() {
    return  {
      appointments: [],
      searchTerms: "",
      aptIndex: 0
    };
  },
  methods: {
    SearchAppointments: function (terms) {
      this.searchTerms = terms;
    }
  }
``` 
- Next we have to filter the arrays based on the search term. For that we add the computed section that Vue.js will always keep a track of. 
```
  computed: {
    searchedApts: function() {
      return this.appointments.filter(item => {
        return(
          item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase()) 
        );
      });
    }
  },
```
- We pass along this computed property in the appointment-list component.
```
  <appointment-list :appointments="searchedApts" @remove="removeItem" @edit="editItem" />
```
- We see that the Search is now working properly, it will look through each of the three fields that we have mentioned and display the results that match.

### Sorting the lists based on different parameters
- We will need a couple of variables in the main component. filterKey which is the name of the variable we want to filter and filterDir which is either asc or desc. 
```
  data: function() {
    return  {
      appointments: [],
      filterKey: "petName",
      filterDir: "asc",
      searchTerms: "",
      aptIndex: 0
    };
  },
```
- Then, we create another computed property called filteredApts and instead of displaying the searchedApt, we will display the filteredApts.
```
  <appointment-list :appointments="searchedApts" @remove="removeItem" @edit="editItem" />

  computed: {
    filteredApts: function () {
      return _.orderBy(
        this.searchedApts,
        item => {
          return item[this.filterKey].toLowerCase();
        }, this.filterDir
      );
    }
  },
```
- On saving and running, we observe that the appointment list is sorted in an ascending order based on the key PetName. We can change the filterKey from Vue developer tools and change the filterDir too and observe that the results show up correctly.

### Updating the dropdown template
- Instead of passing the elements from Vue developer tools, we need to set this via the dropdown that we have in place. We pass the variables filterKey and filterDir from the Main component to the SearchAppointments component.
```
  <search-appointments
    @searchRecords="searchAppointments"
    :myKey="filterKey"
    :myDir="filterDir"
  /> 
```
- myKey and myDir will be the variable names in the seach-appointments sub-component. We receive these in the props.
```
props: ["myKey, myDir"],
```
- Now that we have these values, we use them to control whether or not the checkboxes are showing up or not. we add a v-if check to see if a check boxes should show up or not depending on the myKey and myDir values that are passed from the parent component.
```
  <font-awesome-icon icon="check" v-if="myKey==='petName'"/>
  <font-awesome-icon icon="check" v-if="myKey==='aptDate'"/>
  <font-awesome-icon icon="check" v-if="myKey==='petOwner'"/>
  <font-awesome-icon icon="check" v-if="myDir==='asc'"/>
  <font-awesome-icon icon="check" v-if="myDir==='desc'" />
```

- We can now read the values of direction and filter key correctly and based on those values can display the checkboxes. We need to create events to push a change on clicking these options. We do that by adding the @click which emits the requestKep and field name to the parent component.
```
  <a
    href="#"
    class="dropdown-item d-flex justify-content-between"
    id="petName"
    @click="$emit('requestKey','petName')"
  >
  <a 
    class="dropdown-item d-flex justify-content-between"
    href="#"
    id="aptDate"
    @click="$emit('requestKey','aptDate')"
  >
  <a
    href="#"
    class="dropdown-item d-flex justify-content-between"
    id="ownerName"
    @click="$emit('requestKey','petOwner')"

  >
  <a
    class="dropdown-item d-flex justify-content-between"
    href="#"
    id="asc"
    @click="$emit('requestDir','asc')"
  >
  <a
    class="dropdown-item d-flex justify-content-between"
    href="#"
    id="desc"
    @click="$emit('requestDir','desc')"
  >
```

- Once, we have that set up we need to capture these in the main component.
```
  <search-appointments
    @searchRecords="searchAppointments"
    :myKey="filterKey"
    :myDir="filterDir"
    @request-key="changeKey"
    @request-dir="changeDir"
  /> 
```
- Then we have to update the variables filterKey and filterDir which we do via the methods.
```
  methods: {
    changeKey: function(value) {
      this.filterKey = value;
    },
    changeDir: function(value) {
      this.filterDir = value;
    }
  },
```
- Once we save and run the file we observe that the Sort by dropdown is now funcitonal. The checkboxes are now clickable and results are visible accordingly.
