# dec4rent
An application to find Decathlon rent store.

## Docker
To start project `docker-compose up svelte`.

Use `sh terminal.cmd` to run the node container and use npm command.

Use `docker-compose up e2e` while Svelte service is running for Jasmine unit testing and Cypress end to end testing.

For more reference please see https://github.com/ScienceVikings/svelte-template

## Project setting
<b>framework</b> : Svelte

<b>styling</b> : sass

<b>environment variables</b> : add them inside docker-compose file, then recall them inside rollup.config.js, plugin svelte section. To use this variables inside your project: `process.env.variable_name`

### Components
<b>Hero</b> : banner component, it takes as props an object with the properties <b>title</b>, <b>subtitle</b> and <b>discount</b>.

<b>Searchbar</b> : the search with dkrent api fire on:input. The fulltext endpoint get all results that matches the input in all fields, so I use the js filter function to get only the results with the city that match the input.

If there are no results the google maps search fire
