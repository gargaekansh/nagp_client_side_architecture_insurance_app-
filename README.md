# Insurance Company App 

## 1. Micro-Frontend Architecture Overview

This is a POC of an insurance company app, developed using micro-frontend architecture with React. The application consists of three apps:

### 1.1 Container App
This is the shell/container application responsible for handling the user sign-in/sign-up process and loading the micro-frontends.

### 1.2 Users App
This is a micro-frontend app responsible for displaying the user profile details and checking if the user is eligible for insurance offers.

### 1.3 Insurance App
This is a micro-frontend app responsible for displaying the user's insurance details (existing) and allowing the user to pay the premium.

---

## 2. Features & Functionality

### 2.1 Container App
- Seed the user and insurance data to local storage on startup.
- Show the login page that takes an email address as input.
- **Sign-in button** functionality:
  - Check the email format.
  - Sanitize the input to prevent XSS (Cross-Site Scripting) attacks (OWASP top 10).
  - Check if the user with the given email address exists:
    - If yes, redirect to the landing page and load the user details micro-frontend.
    - If not, stay on the login screen and show an error message.
- Show the menu sidebar with a few buttons/links.
- Display the logged-in user's name at the top.
- **View Profile Details** button will load the user micro-frontend app and display user details.
- **View Insurance Details** button will load the insurance micro-frontend app and show insurance details.
- **Send Message** button will dispatch an event, which will be listened to by both the micro-frontend apps (if already loaded), and lead to displaying a message.
- **Logout Button** will log out the user and redirect to the login screen.

### 2.2 Users App
- Use a background worker to calculate and find the best offers as per the user’s eligibility (e.g., check age, gender, income, and find suitable offers).
- Show the user profile details.
- Listen to the message/event sent from the Container app and display the message accordingly.

-### 2.3 Insurance App
- Uses a background worker to call an API every few seconds and display helpful information on the screen (simulation of an actual API call). The information provides practical tips such as renewal reminders, claim guidance, discount suggestions, and support contacts.
- Show the user’s insurance details.
- On click of the **Pay the Premium** button, show the payment options and enable premium payment.
- On click of the **Cancel** button, hide the payment options.
- Listen to the message/event sent from the Container app and display the message accordingly.

---



---

## 3. Delivery Checklist

| **Requirement**                                    | **Status** |
| -------------------------------------------------- | ---------- |
| High-level design document of the application     |     Provided      |
| Git Link to code for your application (Container app + 2 MFEs) | https://github.com/gargaekansh/nagp_client_side_architecture_insurance_app- |
| Readme file with instructions                     | Provided         |
| Video recording showing all parameters (Running and hosted Containers, MFEs) | Provided          |

---

## 4. How to Run the App

Follow the steps below to set up and run the application:

 - Clone the repository and open it in your IDE:

 ```bash
 git clone https://github.com/gargaekansh/nagp_client_side_architecture_insurance_app-
 cd nagp_client_side_architecture_insurance_app-
 ```

 - Open the code in any IDE like Visual Studio Code.
- You’ll see three folders named `container`, `users`, and `insurance`.
- Open the integrated terminal.
- **Execute the following commands**:

### First run the Users App
```bash
cd users
npm install
npm start
```
##### Users’ app will now be running at http://localhost:3001. Same can be verified in browser.



### Then run the Insurance App
```bash
cd insurance
npm install
npm start
```
##### Insurance app will now be running at http://localhost:3002. Same can be verified in browser.


### And then run the Container App
```bash
cd container
npm install
npm start
```
##### Container app will now be running at http://localhost:3000. Same can be verified in browser.



- All apps are now running. Use the container app running at http://localhost:3000 to validate the functionality.
- Inside the insurance folder under src folder you’ll see a file named seeder.js. Open it and copy any of the email Id from the static user.
- Ender the copied email id on the login screen and click login.


## Please note, having node js and npm installed on your machine is a must to run React app.

## 5. Module Federation remotes (toggle for local vs Netlify)

When running the container that consumes the remotes, toggle the remotes in the container webpack config depending on where the remotes are hosted:

// Uncomment these when hosting remotes locally:
```js
// userdetails: 'userdetails@http://localhost:3001/remoteEntry.js',
// insurancedetails: 'insurancedetails@http://localhost:3002/remoteEntry.js',
```
 
// Uncomment these when hosting remotes on Netlify:

```js
userdetails: 'userdetails@https://nagp-akansh-user.netlify.app/remoteEntry.js',
insurancedetails: 'insurancedetails@https://nagp-akansh-insurance.netlify.app/remoteEntry.js',
```

## 6. Remote Deployment Links (Netlify)
1. Container (main app): https://nagp-akansh-container.netlify.app/
2. Users micro-frontend: https://nagp-akansh-user.netlify.app/
3. Insurance micro-frontend: https://nagp-akansh-insurance.netlify.app/

Note: The container link is the primary entry point for the micro-frontend system. Before building the container for production, update `container/webpack.config.js` remotes to point to the Users and Insurance Netlify URLs.

## 7. GitHub Repository

Repository: https://github.com/gargaekansh/nagp_client_side_architecture_insurance_app-

