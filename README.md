# Learning Vue by Creating a Table and Displaying Data from an API.

## Intoduction

The purpose of this project is to learn how to use Vue and Vuetify by creating a table that displays data from an API. The project will include implementing pagination, sorting, and displaying data/ hyperlinks.

## Tasks

1. Creating a Table using Vuetify
   To create a table, there are two options: v-table and v-data-table. The v-table is a simple table with no extra configuration, while the v-data-table comes with pagination, sorting, and other functions. For this project, we will be using v-table to learn how to work with Vue.

2. Getting Data from the Open Brewery DB API
   We will be getting data from the Open Brewery DB API. The documentation for the API can be found here: https://www.openbrewerydb.org/documentation

3. Displaying Website URLs as Hyperlinks
   From the API, there is a key named "website_url". We will display this as a hyperlink with the target of "\_blink" so that the users can click on the link to visit the website.

4. Showing Only 5 Results per Page

5. Implementing Pagination

6. Implementing Sort by Name
   We will be implementing sorting by name so that users can easily find the information they are looking for. This will allow users to sort the table alphabetically by name.

7. Displaying an Option to Select by Type
   We will display an option where users can select the key "by_type" and display it on the table. This will allow users to filter the table by type, making it easier to find the information they are looking for.

## Tools

- Vue
- Vuetify
- TypeScript

## Installation

1. Clone the repository:

```
git clone https://github.com/LetsCodeManh/vue-table.git
```

2. Install the dependencies:

```
npm install
```

3. Run the app:

```
npm run dev
```