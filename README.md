# SvelteKit + Firebase Full Stack Development

## Overview

This project is a full stack web application built using SvelteKit and Firebase. It includes features like Svelte stores, state management, authentication, routing, styling, and responsive web app development. Additionally, Firebase Authentication and Firestore are used for user authentication and database operations respectively. With this setup, you can easily implement CRUD (Create, Read, Update, Delete) operations for your web application.

_Note: This project is in beta release._

## Setup

1. **Clone the Repository**: Clone this repository to your local machine.

2. **Install Dependencies**: Navigate to the project directory and run `npm install` to install all the necessary dependencies.

3. **Firebase Configuration**:

   - Create a Firebase project on the Firebase console (https://console.firebase.google.com/).
   - Enable Firebase Authentication and Firestore for your project.
   - Obtain your Firebase configuration details (API key, authDomain, projectId, etc.).
   - Update the Firebase configuration in `src/firebase/config.js`.

4. **Run the Application**:
   - Once the setup is complete, run `npm run dev --watch` to start the development server.
   - Open your browser and navigate to `http://localhost:5173` to view the application.

## Features

- **SvelteKit**: Utilizes SvelteKit for building efficient and reactive web applications.
- **Firebase Authentication**: Implements user authentication using Firebase Authentication.
- **Firestore**: Utilizes Firestore for database operations, enabling seamless CRUD operations.
- **Responsive Design**: Built with responsiveness in mind, ensuring optimal viewing experience across devices.
- **Svelte Stores**: Utilizes Svelte stores for managing global application state.
- **Routing**: Implements client-side routing for seamless navigation between pages.
- **Styling**: Provides styling using Svelte's built-in CSS handling capabilities.
- **CRUD Operations**: Easily implement Create, Read, Update, and Delete operations with Firestore.

## Contributing
Contributions are welcome! Feel free to submit issues or pull requests for any improvements or bug fixes.

Contact me via [LinkedIn](https://www.linkedin.com/in/shubham-bane) for any inquiries or discussions regarding the project.

### LICENSE
[MIT License](LICENSE)
