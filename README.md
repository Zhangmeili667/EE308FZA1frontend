# Zhang Minhui's Contact List Front-end Project

## Project Overview

This is a contact list front-end project developed using Vue.js, which allows users to view, search, add, edit, and delete contact information. The project utilizes the Element UI library to build the user interface.

## Features

- **Search Functionality**: Users can search for contacts by name and gender.
- **Add Contacts**: Users can add new contact information.
- **Edit Contacts**: Users can edit existing contact information.
- **Delete Contacts**: Users can delete unwanted contact information.
- **Table Presentation**: Contact information is presented in a table format, including name, number, gender, creation time, and update time.

## Technology Stack

- **Front-end Framework**: Vue.js
- **UI Library**: Element UI
- **State Management**: Not applicable (simple project, no state management library needed)
- **HTTP Client**: Axios

## Project Structure
src/

├── assets/          # Static assets folder

├── components/      # Vue components folder

├── views/           # Vue views folder

├── router/          # Vue router configuration folder

├── store/           # Vuex state management folder (if needed)

└── App.vue          # Main component

└── main.js          # Entry file


## Installation Guide

1. Clone the project to your local machine:
   ```bash
   git clone https://github.com/yourusername/yourproject.git
   ```
   
2. Navigate to the project directory:
   ```bash
   cd yourproject
   ```
3. Install dependencies:
   ```bash
   npm install
   ```
4. Start the development server:
   ```bash
   npm run serve
   ```
## Usage Instructions
**Add Contacts**: Click the "Add Contact" button, fill in the form, and submit.
**Edit Contacts**: Click the "edit" button in the table, modify the form information, and submit.
**Delete Contacts**: Click the "delete" button in the table and confirm the deletion.
**Search Contacts**: Enter a name and gender in the search form and click the "Search" button.

## API Endpoints
The project interacts with backend APIs, and here are some of the main API endpoints:

GET /contacts: Retrieve all contact information.
GET /searchByName?name=xxx&gender=xxx: Search for contacts by name and gender.
POST /contacts: Add new contact information.
POST /updateContact: Update existing contact information.
DELETE /contacts/:id: Delete contact information with a specified ID.

## Notes
Ensure that the backend API service is running so that the front-end project can retrieve data normally.
The project uses the Element UI library; ensure it is correctly installed and configured.
The project is provided as an example; adjustments may be needed based on the backend API for actual deployment.

## Contribution Guidelines
Contributions of any kind are welcome, including code submissions, bug reports, and feature requests. Before submitting code, ensure you follow the project's development standards and code style.
