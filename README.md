# Storyblok Integration Field Starter

> Custom integration field type plugin starter kit; Use this starter kit to make your external APIs available in Storyblok if multi-option and single-option are not enough.

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

Startups local development server running Vue. You will only be able to develop this custom field type by enabling the [local development option](https://www.storyblok.com/docs/Guides/Creating-a-field-type-plugin#how-to-develop-plugins-locally) with Storyblok.

```
npm run serve
```

### Compiles and minifies for production

Exports the final plugin that can be included in Storyblok under `export.js`. Upload its content to your plugin. Make sure that your plugin name configured in `/src/Plugin.vue` is the equal to the name of your actual Storyblok plugin. Each plugin name is globally unqiue, which means that across Storyblok there will only be one plugin with that exact name for all users, even tho not all users will have access to your plugin.

```
npm run build
```

## View: The Integration Selection Overview

The overview of your results will be shown as in the screen below. It will handle pagination generation, the pagination logic needs to be in the API layer. Checkout [How to use this custom field type with your API?](#how-to-use-this-custom-field-type-with-your-api) to find out how you can use it with your API.

![Example selection overview](https://a.storyblok.com/f/39898/3356x1750/d86bee6ad1/integration-field-selection.jpg)

## View: The Selected Value

The selected value will be shown as a box similar to the one you can see in the overview. It will also be marked in the overview itself so editors will see that they have already selected that value.

![One selected value](https://img2.storyblok.com/fit-in/1600x0/filters:fill(ffffff)/f/39898/702x324/e08b453c09/integration-field-selected.jpg)

## How to use this custom field type with your API?

Below you can find the response object expected by this custom field type. With the Storyblok plugin options you can define the key `endpoint` with your API enpoint that should be called. The custom field type will add `per_page`, `page` and if somebody added a search term `search` as query parameter to the call so you can perform the pagination and if needed a search in your API endpoint. If you need authentication, you can configure the Storyblok custom field type option `token` which will be used as username for Basic Authentication.

## Attached Query Params

| Parameter | Description |
|----|----|
| `per_page` | How many results should be returned per page (Default: 50) |
| `page` | Which page is requested (Default: 1) |
| `search` | Debounced search term entered by the user; will not be attached if empty |

- Example without search term: https://mydomain.example/api/integration?per_page=50&page=1
- Example with page 2: https://mydomain.example/api/integration?per_page=50&page=2
- Example with only 10 results per page: https://mydomain.example/api/integration?per_page=10&page=1
- Example with search term: https://mydomain.example/api/integration?per_page=50&page=1&search=Savan

## The Response Object

| Property | Description |
|----|----|
| `results_size` | Total amount of results, used to generate pagination. |
| `results` | Actual results. By default this starter kit uses 50 `per_page`. |

```
{
  "results_size": 123, 
  "results": [
    // multiple integration objects
  ]
}
```

## The Integration Object 

| Property | Description |
|----|----|
| `id` | id of your result |
| `title` | Title that should be shown to the editor during selection |
| `image_url` | If set it will be shown next to the description to make selection for the user easier |
| `last_update` | Timestamp of the latest update of this item |
| `description` | A description that should be displayed below the title. Will automatically be truncated. |
| `blob` | A JSON Object containing more information you want to have stored and available in the Storyblok API after selection |

```
{
  "id": "baf0f820-0fff-456f-9256-0da23bafa481",
  "image_url": "http://placehold.it/150x150",
  "last_update": 1509364426938,
  "title": "Savannah Mcfadden",
  "description": "Eiusmod nisi ut ea et duis consectetur in occaecat non culpa. Sit nisi ut velit non id pariatur in esse enim laboris duis sit. Cillum enim elit nulla labore incididunt. Voluptate eu aute velit culpa est et aute do. Lorem id minim commodo et. Voluptate magna tempor sint cillum aute tempor proident cupidatat sint. Mollit officia non nisi id id nulla exercitation et ullamco ut laboris tempor.",
  "blob": {
    YOUR PROPERTIES
  }
}
```