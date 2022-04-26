# Custom Quasar qselect (custom-quasar-qselect)

Custom Quasar2 QSelect app ver01 2022_0401- April 25,2022

## Install the dependencies

```bash
yarn
# or
npm install
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)

```bash
quasar dev
```

### Lint the files

```bash
yarn lint
# or
npm run lint
```

### Format the files

```bash
yarn format
# or
npm run format
```

### Build the app for production

```bash
quasar build
```

### Customize the configuration

See [Configuring quasar.config.js](https://v2.quasar.dev/quasar-cli-vite/quasar-config-js).

# Dan's added Notes:

version: "0.1.0" Notes;

Demonstrates how to create a qSelect child component using;
vue 3 + Quasar 2 + v-model + Typescript + interface.

In my app, I have a dozen fixed rarely-changing selection lists.
My database contains a table for each of these selections lists.
My admin panel preform CRUD actions to these select database tables.
These database tables always has the same three fields; id, label, and description. This simplifies the
crud UI editors for the different select-tables, as I don't have to create a different ui for each select-database-table.

During the build process, the json optionsArr is generated as
a static array + .vue file and the .vue file is auto-generated into specialized middleware select components.
For example, one select is for allowed color-schemes, another select is a list of features, etc.

## Changed files:

/src/pages/indexPage.vue - Parent Component
/src/components/CustomQselectComponent.vue - custom qSelect child component
/src/components/models.ts - an interface model used by both the parent and child via v-model

## CustomQselectComponent props

props.title: Heading on component

props.qsname: the name prop for the qselect

props.qslabel: The "type of select", like "address" or "Color Scheme"
NOTE: The component changes the label on the qselect as follows;
a) when mounted it is ('Select a ' + props.qslabel + '...')
B) after the user has selected an item, it changes to: (props.qslabel + ':')

props.optionsArr: Array of objects for the select-list. To change the fields in each object, modify the models.ts file.

props.model: contains the results using vue3's v-model's two-way binding.

## future enhancements

Create middleware select components that handles specific select types.
