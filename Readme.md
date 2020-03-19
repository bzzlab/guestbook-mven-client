# Get started with the guestbook application
### Introduction
This guestbook application has been developed with the following technology-stack:
#### Backend (guestbook-mven-server)
* Express.js (middleware, model-view-controller)
* Alasql.js (simple file-based database)
* Node.js (webbased backend infrastructure)

#### Frontend (guestbook-mven-client)
* Vue.js (component-based user-interfaces)
* babel (transpiler, compatibility of new ECMAScript 6 and higher to ECMAScript 5)

>This step-by-step installation handles the backend (guestbook-mven-client)!  

#### Prerequisite
You need to install [nodejs](https://nodejs.org/en/) in order to install the required infrastructure. With the installation of nodejs the tool `npm` (Node package manager) is included.

##### Remarks for MacOS-users
When using  `npm` on the command line the usage differs on Windows and MacOS based platforms.
##### Windows 
On Windows you can use the `npm ...` straight away. Example: 
```
npm install
```
##### MacOS
On MacOS - if you open the terminal as non-administrator - then use it with the `sudo`-command 
Example: 
```
sudo npm install
``` 
and then type  in the administrator password. 
In the following installation guide the `sudo`-command is omitted. But be aware of the if you're an Apple user without default administrator privileges.

### Part 1: Cloning client and installing dependencies
Step 1: Clone the code from this repo from the command-line
```
git clone https://github.com/bzzlab/guestbook-mven-client.git
cd guestbook-mven-client
```
Step 2: Install app dependencies
```
npm install
```

### Part 2: Add program code for getting and posting data (GET and POST-Request)
#### Prerequisite
>The server part (backend) of the guestbook application is completed and fully functional.
When not, then complete the steps of the [backend-part](https://github.com/bzzlab/guestbook-mven-server#get-started-with-the-guestbook-application).

#### Steps
Step 1: Open the project in Webstorm

Step 2: Search for Task-1 and add the code below.
* It lists all *eintraege* from the *guestbookdb* table *eintrag*
```
<!-- Task-1: Add code here -->
<div v-for="eintrag in eintraege">
    <div class="card" style="width: 25rem;">
        <div class="card-body">
            <h5 class="card-title">{{ eintrag.titel }}</h5>
            <h6 class="card-subtitle mb-2 text-muted">From {{ eintrag.autor }}</h6>
            <p class="card-text">{{ eintrag.text }}</p>
        </div>
    </div>
    <div style="margin-bottom: 1rem"></div>
</div>
<!-- Task-End -->
```

Step 3: Search for Task-2 and add the code below. 
* This is an input form as a template in vue.js
```        
<!-- Task-2: Add code here -->
<h4 style="margin-top: 2rem; margin-bottom: 1rem">Post an entry</h4>
<form v-on:submit.prevent="addPost">
    <div class="form-group col-md-6">
        <div class="form-group">
            <label for="autor">Name</label>
            <input v-model="eintrag.autor" type="text" class="form-control" id="autor" placeholder="Name">
        </div>
        <div class="form-group">
            <label for="email">Name</label>
            <input v-model="eintrag.email" type="text" class="form-control" id="email" placeholder="Email">
        </div>
        <div class="form-group">
            <label for="titel">Title</label>
            <input v-model="eintrag.titel" type="text" class="form-control" id="titel" placeholder="Title">
        </div>
        <div class="form-group">
            <label for="text">Text</label>
            <textarea v-model="eintrag.text" class="form-control" id="text" rows="3"/>
        </div>
        <div class="form-group">
            <button type="submit" class="btn btn-primary" data-toggle="modal"
                    data-target="#confirmBlogEntry">Create</button>
        </div>
    </div>
</form>
<!-- Task-End -->
```

Step 4: Search for Task-2b and add the code below. 
* It defines the data that are used for the form. 
* *eintraege* is used as an Array. You can name also *eintragListe* if you prefer.
* *eintrag* is used for fetching data from input-form and sending them (in JSON format) 
to the server (POST method) and finally storing into the database or ... 
* when getting data from the server (GET method) and showing on the client

```        
//Task-3: Add code here
name: "GuestbookCreate",
data: () => ({
    message: null,
    eintraege: null,
    eintrag: {
        titel: "",
        text: "",
        autor: "",
        email: "",
        datum: ""
    }
}),
//Task-End
```

Step 5: Search for Task-2c and add the code below. 
* Post method which is triggered by the submit button
```        
//Task-4: Add code here
 addPost(){
     fetch(API_URL +'/api/blog',
         {
             method: 'POST',
             body: JSON.stringify(this.eintrag),
             headers: {"content-type":"application/json"}
         })
         .then(res => res.json());
     this.proceed();
 },
 //Task-End
```

### Part 3: Build
#### Steps
Step 1: Build application from Webstorm or from the console 
```
npm run built-client
```
>No error (red colored messages) should appear!

## Part 4: Test
Step 1: Run the server. If you don't know how then go to the [Readme - Part 3](https://github.com/bzzlab/guestbook-mven-server#part-3-build)
Step 2: Run application from Webstorm or from the console
```
npm run run-client
```


