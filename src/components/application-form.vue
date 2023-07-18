<template>
  <router-link to="/">Back</router-link>
  <div v-if="isValidUrl" class="showForm">
    <fieldset class="card" style="width: 50rem">
      <legend class="card-header">Basic Details :</legend>

      <table>
        <tr>
          <td><label for=""> FirstName :</label></td>
          <td>
            <input v-model="form.firstName" type="text" />
          </td>

          <td><label for="">LastName :</label></td>
          <td>
            <input v-model="form.lastName" type="text" />
          </td>
        </tr>
        <tr>
          <td><label for=""> Designation :</label></td>
          <td>
            <input v-model="form.designation" type="text" />
          </td>

          <td><label for="">Email :</label></td>
          <td>
            <input v-model="form.email" type="email" />
          </td>
        </tr>

        <tr>
          <td><label for="">Address 1 :</label></td>
          <td>
            <textarea rows="2" cols="17" v-model="form.address1">
Enter text here...</textarea
            >
          </td>

          <td><label for=""> Address 2 :</label></td>
          <td>
            <textarea rows="2" cols="17" v-model="form.address2">
Enter text here...</textarea
            >
          </td>
        </tr>
        <tr>
          <td><label for="">State :</label></td>
          <td>
            <select v-model="form.state">
              <option
                v-for="el in stateAndCity"
                :key="el.state"
                :value="el.state"
              >
                {{ el.state }}
              </option>
            </select>
          </td>
          <td><label for="">City :</label></td>
          <td>
            <select v-model="form.city">
              <option v-for="el in currentCityOptions" :key="el" :value="el">
                {{ el }}
              </option>
            </select>
          </td>
        </tr>

        <tr>
          <td><label for="">PhoneNumber :</label></td>
          <td>
            <input type="text" v-model="form.phoneNumber" />
          </td>
          <td><label for="">Gender :</label></td>
          <td>
            <input type="radio" v-model="form.gender" value="male" />Man
            <input type="radio" v-model="form.gender" value="female" />Woman
          </td>
        </tr>

        <tr>
          <td><label for="">RelationShip Status :</label></td>
          <td>
            <select v-model="form.relationship">
              <option value="single">Single</option>
              <option value="Married">Married</option>
            </select>
          </td>

          <td><label for="">Date Of Birth :</label></td>
          <td>
            <input type="date" name="date" id="date" v-model="form.date" />
          </td>
        </tr>
      </table>
    </fieldset>
    <div class="education">
      <fieldset class="card" style="width: 47rem">
        <legend class="card-header">Education Detail :</legend>
        <table>
          <div class="add-div">
            <button type="button" @click="addEducation()" class="add-btn">
              Add Row
            </button>
          </div>

          <tr v-for="(el, index) in form.educationDetails" :key="index">
            <td>
              Education:<select v-model="el.educationOption">
                <option
                  v-for="option in educationOptions"
                  :key="option"
                  :value="option"
                >
                  {{ option }}
                </option>
              </select>
            </td>
            <td>Course Name: <input v-model="el.course" type="text" /></td>
            <td>University :<input v-model="el.university" type="text" /></td>
            <td>
              Passing Year : <input v-model="el.passingYear" type="text" />
            </td>

            <td v-if="form.educationDetails.length > 1">
              <button
                type="button"
                @click="removeEducation(index)"
                class="remove-btn"
              >
                Remove
              </button>
            </td>
          </tr>
        </table>
      </fieldset>
      <fieldset class="card" style="width: 46rem">
        <legend class="card-header">Work Experience :</legend>
        <div class="add-div">
          <button type="button" @click="addWork" class="add-btn">
            Add Row
          </button>
        </div>

        <table>
          <tr v-for="(field, index) in form.workExperience" :key="index">
            <td>
              Company Name:
              <input v-model="field.company" type="text" />
            </td>
            <td>
              Designation :
              <input v-model="field.designation" type="text" />
            </td>
            <td>
              From :
              <input type="date" v-model="field.from" />
            </td>
            <td>
              To :
              <input type="date" v-model="field.to" />
            </td>

            <td v-if="form.workExperience.length > 1">
              <button
                type="button"
                @click="removeWork(index)"
                class="remove-btn"
              >
                Remove
              </button>
            </td>
            &nbsp;&nbsp;
          </tr>
        </table>
      </fieldset>
    </div>

    <div class="language">
      <fieldset class="card" style="width: 30rem">
        <legend class="card-header">Language Known :</legend>
        <table>
          <div class="add-div">
            <button type="button" @click="addLanguage" class="add-btn">
              Add Row
            </button>
          </div>

          <tr v-for="(field, index) in form.languageKnown" :key="index">
            <td>
              <select v-model="field.language">
                <option
                  v-for="option in langOptions"
                  :key="option"
                  :value="option"
                >
                  {{ option }}
                </option>
              </select>
            </td>
            <td v-for="(option, i) in langKnownOptions" :key="i">
              <input
                type="checkbox"
                v-model="field.selectedLang"
                :id="option"
                :value="option"
              />
              <label :for="option">{{ option }}</label>
            </td>

            <td v-if="form.languageKnown.length > 1">
              <button
                type="button"
                @click="removeLanguage(index)"
                class="remove-btn"
              >
                Remove
              </button>
            </td>
          </tr>
        </table>
      </fieldset>

      <fieldset class="card" style="width: 30rem">
        <legend class="card-header">Technologies you know :</legend>
        <table>
          <div class="add-div">
            <button @click="addTechnology" type="button" class="add-btn">
              Add Row
            </button>
          </div>

          <tr v-for="(field, index) in form.technologyKnow" :key="index">
            <td>
              <select v-model="field.techOption">
                <option
                  v-for="option in technologyOptions"
                  :key="option"
                  :value="option"
                >
                  {{ option }}
                </option>
              </select>
            </td>

            <td v-for="(option, i) in techKnownOptions" :key="i">
              <input
                type="radio"
                v-model="field.selectedTechKnown"
                :id="option"
                :value="option"
              />
              <label :for="option">{{ option }}</label>
            </td>

            <td v-if="form.technologyKnow.length > 1">
              <button
                type="button"
                @click="removeTechnology(index)"
                class="remove-btn"
              >
                Remove
              </button>
            </td>
          </tr>
        </table>
      </fieldset>
    </div>

    <fieldset class="card" style="width: 57rem">
      <legend class="card-header">Reference Contact :</legend>
      <table>
        <div class="add-div">
          <button type="button" @click="addContact" class="add-btn">
            Add Row
          </button>
        </div>

        <tr v-for="(field, index) in form.refContact" :key="index">
          <td>
            Name :

            <input v-model="field.contactName" type="text" />
          </td>
          <td>
            Contact Number :

            <input v-model="field.contactNumber" type="text" />
          </td>
          <td>
            Relation :

            <input v-model="field.relation" type="text" />
          </td>

          <td v-if="form.refContact.length > 1">
            <button
              type="button"
              @click="removeContact(index)"
              class="remove-btn"
            >
              Remove
            </button>
          </td>
          &nbsp;&nbsp;
        </tr>
      </table>
    </fieldset>

    <fieldset class="card" style="width: 57rem">
      <legend class="card-header">Preferences :</legend>
      <table align="center">
        <tr>
          <td rowspan="6"><label for="">Preferred location :</label></td>
          <td rowspan="6">
            <select v-model="form.preferredLocation" multiple>
              <option
                v-for="option in departmentOption"
                :key="option"
                :value="option"
              >
                {{ option }}
              </option>
            </select>
          </td>

          <td><label for="">Notice period :</label></td>
          <td>
            <input v-model="form.noticePeriod" type="text" />
          </td>

          <td><label for="">Department :</label></td>
          <td>
            <select v-model="form.department">
              <option
                v-for="option in departmentOption"
                :key="option"
                :value="option"
              >
                {{ option }}
              </option>
            </select>
          </td>
        </tr>

        <tr>
          <td><label for="">Expected CTC :</label></td>
          <td>
            <input v-model="form.expectedCtc" type="text" />
          </td>
        </tr>

        <tr>
          <td><label for="">Current CTC :</label></td>
          <td>
            <input v-model="form.currentCtc" type="text" />
          </td>
        </tr>
      </table>
    </fieldset>
    <button type="button" class="submit" @click="onClickSubmit()">
      Submit
    </button>
  </div>
  <div v-else>Invalid url, Please try again</div>
</template>

<script>
import { ref, onBeforeMount, computed } from "vue";
import { useRoute } from "vue-router";
export default {
  name: "ApplicationForm",
  setup() {
    const stateAndCity = [
      { state: "Gujarat", city: ["Rajkot", "Ahmedabad", "Surat"] },
      { state: "Rajasthan", city: ["Jaipur", "Udaipur", "Ajmer"] },
      { state: "Maharastra", city: ["Mumbai", "Pune", "Nasik"] },
    ];
    const educationOptions = ["SSC", "HSC", "Bachelor Degree", "Master Degree"];
    const langOptions = ["Hindi", "English", "Gujarati"];
    const langKnownOptions = ["Read", "Write", "Speak"];
    const technologyOptions = ["PHP", "MySql", "Laravel", "Oracle"];
    const techKnownOptions = ["Beginer", "Mideator", "Expert"];
    const locationOption = ["Rajkot", "Ahmedabad", "Surat"];
    const departmentOption = ["Development", "Marketing", "Design"];
    const userDataArr = ref([]);
    const route = useRoute();
    const isValidUrl = ref(false);

    const form = ref({
      _id: (Math.floor(Math.random() * 90000) + 10000).toString(),
      firstName: null,
      lastName: null,
      designation: null,
      email: null,
      address1: null,
      address2: null,
      phoneNumber: null,
      city: null,
      state: stateAndCity[0].state,
      gender: "female",
      relationship: "single",
      date: null,

      educationDetails: [
        {
          course: null,
          university: null,
          passingYear: null,
          educationOption: educationOptions[0],
        },
      ],

      workExperience: [
        {
          company: null,
          designation: null,
          from: null,
          to: null,
        },
      ],

      languageKnown: [
        {
          language: langOptions[0],
          selectedLang: [],
        },
      ],

      technologyKnow: [
        {
          techOption: technologyOptions[0],
          selectedTechKnown: techKnownOptions[0],
        },
      ],

      refContact: [
        {
          contactName: null,
          contactNumber: null,
          relation: null,
        },
      ],
      preferredLocation: [],
      noticePeriod: null,
      department: departmentOption[0],
      expectedCtc: null,
      currentCtc: null,
    });
    onBeforeMount(() => {
      // const routeData = { ...route };
      const getData = JSON.parse(window.localStorage.getItem("submitValue"));

      if (getData?.length) userDataArr.value = getData;

      if (route?.params?.uid && route.name === "update") {
        userDataArr.value?.forEach((el) => {
          if (el._id === route?.params?.uid) {
            isValidUrl.value = true;
            form.value = el;
          }
        });
      } else if (route.name === "add") isValidUrl.value = true;
      else isValidUrl.value = false;
    });
    const onClickSubmit = () => {
      if (route.name === "update") {
        console.log("uppppppp");
        userDataArr.value?.forEach((el) => {
          if (el._id === form.value._id) {
            el = form.value;
          }
        });
      } else {
        form.value._id = (Math.floor(Math.random() * 90000) + 10000).toString();

        userDataArr.value.push({ ...form.value });
      }
      window.localStorage.setItem(
        "submitValue",
        JSON.stringify(userDataArr.value)
      );
    };

    const currentCityOptions = computed(() => {
      const data = stateAndCity.filter((el) => el.state === form.value.state);
      return data?.[0]?.city;
    });

    const addEducation = () => {
      // form.value.educationDetails.forEach((el) => {
      //   if (educationOptions.value.includes(el.educationOption)) {
      //     educationOptions.value = educationOptions.value.filter(
      //       (val) => val !== el.educationOption
      //     );
      //   }
      // });
      form.value.educationDetails.push({
        course: null,
        university: null,
        passingYear: null,
        educationOption: educationOptions[0],
      });
    };

    const removeEducation = (i) => {
      form.value.educationDetails = form.value.educationDetails.filter(
        (el, index) => index !== i
      );
    };

    const addWork = () => {
      form.value.workExperience.push({
        company: null,
        designation: null,
        from: null,
        to: null,
      });
    };

    const removeWork = (i) => {
      form.value.workExperience = form.value.workExperience.filter(
        (el, index) => index !== i
      );
    };

    const addLanguage = () => {
      form.value.languageKnown.push({
        language: langOptions[0],
        selectedLang: [],
      });
    };

    const removeLanguage = (i) => {
      form.value.languageKnown = form.value.languageKnown.filter(
        (el, index) => index !== i
      );
    };

    const addTechnology = () => {
      form.value.technologyKnow.push({
        techOption: technologyOptions[0],
        selectedTechKnown: techKnownOptions[0],
      });
    };

    const removeTechnology = (i) => {
      form.value.technologyKnow = form.value.technologyKnow.filter(
        (el, index) => index !== i
      );
    };

    const addContact = () => {
      form.value.refContact.push({
        contactName: null,
        contactNumber: null,
        relation: null,
      });
    };

    const removeContact = (i) => {
      form.value.refContact = form.value.refContact.filter(
        (el, index) => index !== i
      );
    };

    return {
      onClickSubmit,
      isValidUrl,
      stateAndCity,
      form,
      currentCityOptions,
      educationOptions,
      addEducation,
      removeEducation,
      addWork,
      removeWork,
      langOptions,
      langKnownOptions,
      addLanguage,
      removeLanguage,
      techKnownOptions,
      technologyOptions,
      addTechnology,
      removeTechnology,
      addContact,
      removeContact,
      locationOption,
      departmentOption,
    };
  },
};
</script>

<style scoped lang="scss">
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  text-align: left;
  padding: 8px;
}

// tr:nth-child(even) {
//   background-color: #dddddd;
// }
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
  padding: 8px 16px;
  text-decoration: none;
}
.showForm {
  display: grid;
  place-items: center;
}

.education,
.language {
  display: flex;
}

fieldset {
  margin-top: 20px;
  background: #fde6f8;
  color: #1c3573;
}
legend {
  padding: 4px 9px;
  border-radius: 12px;
  background: #75498d;
  color: white;
}

.add-div {
  width: 120px;
  .add-btn {
    cursor: pointer;
    border-radius: 4px;
    background-color: #878485;
    color: white;
    padding: 3px 5px;
    border: none;
    margin-left: -40px;
    // #be5c84
  }
}

.remove-btn {
  cursor: pointer;
  border-radius: 4px;
  background-color: #cc5886;
  color: white;
  padding: 4px 4px;
  border: none;
}

.submit {
  margin-top: 10px;
  cursor: pointer;
  border-radius: 4px;
  background-color: #7c6a0df5;
  color: white;
  padding: 12px 19px;
  border: none;
  font-size: 100%;
}
</style>
