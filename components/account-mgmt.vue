<template>
    <div v-if="isLoading" class="pl-72">
        <loading-indicator :Message="message" />
    </div>
    <div v-else>
    <header-text headerText="Your Profile" subHeaderText="Update details and shopping lists to help our grocers understand your needs."/>
    <form style="padding: 50px; background-color: white; border-radius: 10px; box-shadow: 1px 5px 8px grey; margin-left: 350px; margin-right: 50px;">
      <div class="space-y-12">
        <div class="border-b border-gray-900/10 pb-12">
          <h2 class="text-4xl font-semibold leading-7 text-gray-900">Account Management</h2><br>
          <p class="mt-1 text-sm leading-6 text-gray-600">This information will be used for your user account / profile.</p>
    
          <div class="mt-10 grid grid-cols-1 gap-x-6 gap-y-8 sm:grid-cols-6">
            <div class="sm:col-span-4">
              <label for="userId" class="block text-sm font-medium leading-6 text-gray-900">User ID</label>
              <div class="mt-2">
                <input v-model="userId" style="padding-left: 10px" disabled type="text" name="userId" id="userId" autocomplete="userId" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
              </div>
            </div>
    
            <div class="sm:col-span-3">
              <label for="firstName" class="block text-sm font-medium leading-6 text-gray-900">First name</label>
              <div class="mt-2">
                <input v-model="firstName" style="padding-left: 10px" type="text" name="firstName" id="firstName" autocomplete="firstName" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
              </div>
            </div>
    
            <div class="sm:col-span-3">
              <label for="surname" class="block text-sm font-medium leading-6 text-gray-900">Last name</label>
              <div class="mt-2">
                <input v-model="surname" style="padding-left: 10px" type="text" name="surname" id="surname" autocomplete="surname" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
              </div>
            </div>
    
            <div class="sm:col-span-6">
              <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
              <div class="mt-2">
                <input v-model="email" style="padding-left: 10px" id="email" name="email" type="email" autocomplete="email" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
              </div>
            </div>
          </div>
        </div>
    
        <div class="border-b border-gray-900/10 pb-12">
          <h2 class="text-4xl font-semibold leading-7 text-gray-900">Address Information</h2><br>
    
          <div class="mt-10 grid grid-cols-1 gap-x-6 gap-y-8 sm:grid-cols-6">
            <div class="sm:col-span-3">
                <label for="country" class="block text-sm font-medium leading-6 text-gray-900">Country</label>
                <div class="mt-2">
                  <select v-model="country" id="country" name="country" autocomplete="country-name" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:max-w-xs sm:text-sm sm:leading-6">
                    <option>Afghanistan</option>
                    <option>Albania</option>
                    <option>Algeria</option>
                    <option>Andorra</option>
                    <option>Angola</option>
                    <option>Antigua and Barbuda</option>
                    <option>Argentina</option>
                    <option>Armenia</option>
                    <option>Australia</option>
                    <option>Austria</option>
                    <option>Azerbaijan</option>
                    <option>Bahamas</option>
                    <option>Bahrain</option>
                    <option>Bangladesh</option>
                    <option>Barbados</option>
                    <option>Belarus</option>
                    <option>Belgium</option>
                    <option>Belize</option>
                    <option>Benin</option>
                    <option>Bhutan</option>
                    <option>Bolivia</option>
                    <option>Bosnia and Herzegovina</option>
                    <option>Botswana</option>
                    <option>Brazil</option>
                    <option>Brunei</option>
                    <option>Bulgaria</option>
                    <option>Burkina Faso</option>
                    <option>Burundi</option>
                    <option>Cabo Verde</option>
                    <option>Cambodia</option>
                    <option>Cameroon</option>
                    <option>Canada</option>
                    <option>Central African Republic</option>
                    <option>Chad</option>
                    <option>Chile</option>
                    <option>China</option>
                    <option>Colombia</option>
                    <option>Comoros</option>
                    <option>Congo</option>
                    <option>Costa Rica</option>
                    <option>Cote d'Ivoire</option>
                    <option>Croatia</option>
                    <option>Cuba</option>
                    <option>Cyprus</option>
                    <option>Czech Republic</option>
                    <option>Denmark</option>
                    <option>Djibouti</option>
                    <option>Dominica</option>
                    <option>Dominican Republic</option>
                    <option>Ecuador</option>
                    <option>Egypt</option>
                    <option>El Salvador</option>
                    <option>Equatorial Guinea</option>
                    <option>Eritrea</option>
                    <option>Estonia</option>
                    <option>Eswatini</option>
                    <option>Ethiopia</option>
                    <option>Fiji</option>
                    <option>Finland</option>
                    <option>France</option>
                    <option>Gabon</option>
                    <option>Gambia</option>
                    <option>Georgia</option>
                    <option>Germany</option>
                    <option>Ghana</option>
                    <option>Greece</option>
                    <option>Grenada</option>
                    <option>Guatemala</option>
                    <option>Guinea</option>
                    <option>Guinea-Bissau</option>
                    <option>Guyana</option>
                    <option>Haiti</option>
                    <option>Honduras</option>
                    <option>Hungary</option>
                    <option>Iceland</option>
                    <option>India</option>
                    <option>Indonesia</option>
                    <option>Iran</option>
                    <option>Iraq</option>
                    <option>Ireland</option>
                    <option>Israel</option>
                    <option>Italy</option>
                    <option>Jamaica</option>
                    <option>Japan</option>
                    <option>Jordan</option>
                    <option>Kazakhstan</option>
                    <option>Kenya</option>
                    <option>Kiribati</option>
                    <option>Korea, North</option>
                    <option>Korea, South</option>
                    <option>Kosovo</option>
                    <option>Kuwait</option>
                    <option>Kyrgyzstan</option>
                    <option>Laos</option>
                    <option>Latvia</option>
                    <option>Lebanon</option>
                    <option>Lesotho</option>
                    <option>Liberia</option>
                    <option>Libya</option>
                    <option>Liechtenstein</option>
                    <option>Lithuania</option>
                    <option>Luxembourg</option>
                    <option>Madagascar</option>
                    <option>Malawi</option>
                    <option>Malaysia</option>
                    <option>Maldives</option>
                    <option>Mali</option>
                    <option>Malta</option>
                    <option>Marshall Islands</option>
                    <option>Mauritania</option>
                    <option>Mauritius</option>
                    <option>Mexico</option>
                    <option>Micronesia</option>
                    <option>Moldova</option>
                    <option>Monaco</option>
                    <option>Mongolia</option>
                    <option>Montenegro</option>
                    <option>Morocco</option>
                    <option>Mozambique</option>
                    <option>Myanmar</option>
                    <option>Namibia</option>
                    <option>Nauru</option>
                    <option>Nepal</option>
                    <option>Netherlands</option>
                    <option>New Zealand</option>
                    <option>Nicaragua</option>
                    <option>Niger</option>
                    <option>Nigeria</option>
                    <option>North Macedonia</option>
                    <option>Norway</option>
                    <option>Oman</option>
                    <option>Pakistan</option>
                    <option>Palau</option>
                    <option>Panama</option>
                    <option>Papua New Guinea</option>
                    <option>Paraguay</option>
                    <option>Peru</option>
                    <option>Philippines</option>
                    <option>Poland</option>
                    <option>Portugal</option>
                    <option>Qatar</option>
                    <option>Romania</option>
                    <option>Russia</option>
                    <option>Rwanda</option>
                    <option>Saint Kitts and Nevis</option>
                    <option>Saint Lucia</option>
                    <option>Saint Vincent and the Grenadines</option>
                    <option>Samoa</option>
                    <option>San Marino</option>
                    <option>Sao Tome and Principe</option>
                    <option>Saudi Arabia</option>
                    <option>Senegal</option>
                    <option>Serbia</option>
                    <option>Seychelles</option>
                    <option>Sierra Leone</option>
                    <option>Singapore</option>
                    <option>Slovakia</option>
                    <option>Slovenia</option>
                    <option>Solomon Islands</option>
                    <option>Somalia</option>
                    <option>South Africa</option>
                    <option>South Sudan</option>
                    <option>Spain</option>
                    <option>Sri Lanka</option>
                    <option>Sudan</option>
                    <option>Suriname</option>
                    <option>Sweden</option>
                    <option>Switzerland</option>
                    <option>Syria</option>
                    <option>Taiwan</option>
                    <option>Tajikistan</option>
                    <option>Tanzania</option>
                    <option>Thailand</option>
                    <option>Timor-Leste</option>
                    <option>Togo</option>
                    <option>Tonga</option>
                    <option>Trinidad and Tobago</option>
                    <option>Tunisia</option>
                    <option>Turkey</option>
                    <option>Turkmenistan</option>
                    <option>Tuvalu</option>
                    <option>Uganda</option>
                    <option>Ukraine</option>
                    <option>United Arab Emirates</option>
                    <option>United Kingdom</option>
                    <option>United States</option>
                    <option>Uruguay</option>
                    <option>Uzbekistan</option>
                    <option>Vanuatu</option>
                    <option>Vatican City</option>
                    <option>Venezuela</option>
                    <option>Vietnam</option>
                    <option>Yemen</option>
                    <option>Zambia</option>
                    <option>Zimbabwe</option>
                  </select>
                </div>
              </div>
    
              <div class="col-span-full">
                <label for="streetAddress" class="block text-sm font-medium leading-6 text-gray-900">Street address</label>
                <div class="mt-2">
                  <input v-model="streetAddress" style="padding-left: 10px" type="text" name="streetAddress" id="streetAddress" autocomplete="streetAddress" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
                </div>
              </div>
    
              <div class="sm:col-span-2 sm:col-start-1">
                <label for="city" class="block text-sm font-medium leading-6 text-gray-900">City</label>
                <div class="mt-2">
                  <input v-model="city" style="padding-left: 10px" type="text" name="city" id="city" autocomplete="address-level2" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
                </div>
              </div>
    
              <div class="sm:col-span-2">
                <label for="region" class="block text-sm font-medium leading-6 text-gray-900">State / Province</label>
                <div class="mt-2">
                  <input v-model="region" style="padding-left: 10px" type="text" name="region" id="region" autocomplete="address-level1" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
                </div>
              </div>
    
              <div class="sm:col-span-2">
                <label for="postalCode" class="block text-sm font-medium leading-6 text-gray-900">ZIP / Postal code</label>
                <div class="mt-2">
                  <input v-model="postalCode" style="padding-left: 10px" type="text" name="postalCode" id="postalCode" autocomplete="postalCode" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-deep-purple-accent-400 sm:text-sm sm:leading-6" />
                </div>
              </div>
            </div>
        </div>
    
        <div class="border-b border-gray-900/10 pb-12">
          <h2 class="text-4xl font-semibold leading-7 text-gray-900">Notifications</h2><br>
          <p class="mt-1 text-sm leading-6 text-gray-600">We'll always let you know about important changes, but you pick what else you want to hear about.</p>
    
          <div class="mt-10 space-y-10">
            <fieldset>
              <legend class="text-sm font-semibold leading-6 text-gray-900">By Email</legend>
              <div class="mt-6 space-y-6">
                <div class="relative flex gap-x-3">
                  <div class="flex h-6 items-center">
                    <input v-model="purchases" id="purchases" name="purchases" type="checkbox" class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-deep-purple-accent-400" />
                  </div>
                  <div class="text-sm leading-6">
                    <label for="purchases" class="font-medium text-gray-900">Purchases</label>
                    <p class="text-gray-500">Get notified about any purchases, failures or warning notifications.</p>
                  </div>
                </div>
                <div class="relative flex gap-x-3">
                  <div class="flex h-6 items-center">
                    <input v-model="shipping" id="shipping" name="shipping" type="checkbox" class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-deep-purple-accent-400" />
                  </div>
                  <div class="text-sm leading-6">
                    <label for="shipping" class="font-medium text-gray-900">Suggestions</label>
                    <p class="text-gray-500">Get notified about new suggestions that might take your interest.</p>
                  </div>
                </div>
                <div class="relative flex gap-x-3">
                  <div class="flex h-6 items-center">
                    <input v-model="stores" id="stores" name="stores" type="checkbox" class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-deep-purple-accent-400" />
                  </div>
                  <div class="text-sm leading-6">
                    <label for="stores" class="font-medium text-gray-900">Alerts</label>
                    <p class="text-gray-500">Get notified about new alerts appearing on your account.</p>
                  </div>
                </div>
              </div>
            </fieldset>
          </div>
        </div>
      </div>
    
      <div class="mt-6 flex items-center justify-end gap-x-6">
        <form style="width: 100%;" @submit.prevent="setUserData">
          <button type="submit" class="rounded-md bg-blue-400 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Save</button>
        </form>
      </div>
    </form>
  </div>
    </template>
    <script setup lang="js">
    import { ref } from 'vue';
    const userId = ref('');
    const firstName = ref('');
    const surname = ref('');
    const email = ref('');
    const country = ref('');
    const streetAddress = ref('');
    const city = ref('');
    const region = ref('');
    const postalCode = ref('');
    const purchases = ref('');
    const shipping = ref('');
    const stores = ref('');
    const isLoading = ref(true);
    const message = ref('Collecting user information...')
    
    async function getUserData () {
      try {
        const response = await fetch(`https://localhost:7249/api/UserAccount/Get/`+ sessionStorage.getItem('334_group_user_userId'), {
          credentials: 'include'
        });
        const data = await response.json();
        isLoading.value = false;
        return data;
      } catch (error) {
        console.error('Error in getUserData:', error)
      }
    }
    
    async function setUserData () {
      const userData = {
        Id: sessionStorage.getItem('334_group_user_userId'),
        givenName: firstName.value,
        surname: surname.value,
        displayName: firstName.value + " " + surname.value,
        email: email.value,
        street: streetAddress.value,
        city: city.value,
        state: region.value,
        postalCode: postalCode.value,
        country: country.value,
        purchaseNotifications: purchases.value,
        shippingNotifications: shipping.value,
        storeNotifications: stores.value
      }
    
      try {
        const response = await fetch(`https://localhost:7249/api/UserAccount/Update/`+ sessionStorage.getItem('334_group_user_userId'), {
          method: 'PUT',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(userData),
        });
    
        await response;
        window.location.reload();
      } catch (error) {
        console.error('Error in setUserData:', error);
        throw error;
      }
    }
    
    (async () => {
      try {
        const userData = await getUserData();
        userId.value = userData.id;
        firstName.value = userData.givenName;
        surname.value = userData.surname;
        email.value = userData.email;
        streetAddress.value = userData.street;
        city.value  = userData.city;
        region.value = userData.state;
        postalCode.value = userData.postalCode;
        country.value = userData.country;
        purchases.value = userData.purchaseNotifications;
        shipping.value = userData.shippingNotifications;
        stores.value = userData.storeNotifications;
      } catch (error) {
        console.error('Error fetching user data:', error);
      }
    })();
    
    </script>