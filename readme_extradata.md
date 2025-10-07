# matter-extradata

Matter-extradata muestra información adicional sobre un contenido, como el responsable, la fecha de última actualización y opciones de descarga o suscripción. Forma parte del catálogo corporativo de Web Components de la Junta de Andalucía.

## Instalación y servidor de desarrollo

Para levantar el web component en local, se deberá seguir una serie de pasos en el orden correcto, ya que si no, no se podrá iniciar correctamente. Los pasos que se deben seguir son los siguientes:

1. Eliminar el fichero `.npmrc` para así eliminar los repositorios y usuarios almacenados y actualizarlos con los datos necesarios correctos.
    ```bash
    rm C:\Users\{{USER}}\.npmrc
    ```

2. Acceder al [repositorio de web-components del MSD](https://gitlab.juntadeandalucia.es/pt-exp-webcomponents) y seleccionar el que se necesite.
3. Clicar en el botón **"Clone"** y copiar el enlace HTTPS.
4. En local, posicionarse en la carpeta donde se quiera descargar el web-component y abrir una consola de comandos. A continuación, ejecutar el siguiente comando:
    ```bash
    git clone {{enlace HTTPS copiado}}
    ```
    Tras la ejecución de este comando, se habrá creado la carpeta del proyecto `matter-extradata`.
5. Configurar el registro privado de los componentes corporativos:
    ```bash
    npm config set @matter:registry=https://nexus.paas.junta-andalucia.es/repository/msd.npm-private/
    ```
6. Instalar las dependencias del web component:
    ```bash
    npm i
    ```
7. Levantar el proyecto con el servidor de desarrollo de webpack:
    ```bash
    npm start
    ```
8. El proyecto se podrá visualizar en tiempo real en la siguiente ruta:  
   👉 [http://localhost:3000/](http://localhost:3000/)

---

## Uso

Para hacer uso de este web-component se deberán realizar dos sencillos pasos:

1. Importar el compilado del web-component en el proyecto actual:
    ```bash
    import '@matter/matter-extradata/dist/matter-extradata';
    ```
2. Llamar a dicho web-component desde el fichero `.html` donde se quiera mostrar:
    ```html
    <matter-extradata></matter-extradata>
    ```

---

## Ejemplo de uso

```html
<matter-extradata
  idElement="extra-info"
  responsable='{"nombre": "Consejería", "url": "https://example.com"}'
  ultimaActualizacion="29 de Julio de 2025"
  descargas='[
    { "icon": "fa-file-csv", "text": "CSV", "link": "#" },
    { "icon": "fa-file-pdf", "text": "PDF", "link": "#" }
  ]'
  suscripciones='[
    { "icon": "fa-envelope", "text": "Correo", "link": "#" },
    { "icon": "fa-rss", "text": "RSS", "link": "#" }
  ]'
></matter-extradata>
```

---

## Props

| Prop                 | Tipo     | Descripción                                                                                   |
| :------------------- | :------- | :-------------------------------------------------------------------------------------------- |
| `stylesheetVersion`  | string   | Versión de la hoja de estilos a usar. Por defecto `"latest"`.                                |
| `idElement`          | string   | Identificador único del bloque de información adicional.                                     |
| `responsable`        | object   | Objeto con el nombre y la URL del responsable. Ejemplo: `{ "nombre": "Junta de Andalucía", "url": "#" }`. |
| `ultimaActualizacion`| string   | Fecha de la última actualización.                                                            |
| `descargas`          | array    | Lista de objetos con opciones de descarga. Ejemplo: `[ { "icon": "fa-file-pdf", "text": "PDF", "link": "#" } ]`. |
| `suscripciones`      | array    | Lista de objetos con opciones de suscripción. Ejemplo: `[ { "icon": "fa-rss", "text": "RSS", "link": "#" } ]`. |

---

## Edición

Si usas **VS Code**, recomendamos la instalación del plugin [lit-plugin extension](https://marketplace.visualstudio.com/items?itemName=runem.lit-plugin), que ayuda a crear plantillas usando **lit-html**.

Este web component, como todos los del catálogo de la Junta de Andalucía, está desarrollado con [JavaScript](https://www.javascript.com/) y [Lit](https://lit.dev).

---

## Linting

Se usa **ESLint** para comprobar la calidad del código JavaScript.

Configuración basada en la guía de estilo de Airbnb ([.eslintrc.js](./.eslintrc.js))  
Más información [aquí](https://www.npmjs.com/package/eslint-config-airbnb)

Para ejecutar eslint:
```bash
npm run lint
```

---

## Formato

Se utiliza [Prettier](https://prettier.io/) para formatear el código según el estilo del proyecto Polymer.  
Puedes ajustar las reglas en `.prettierrc.json`.

---

## StoryBook

Para añadir una historia al Storybook corporativo, se deben realizar los siguientes pasos:

1. En el fichero `package.json`, añadir el campo:
    ```json
    "type": "moleculas",
    ```
2. En el mismo `package.json`, incluir el plugin `copy-webpack-plugin`:
    ```json
    "devDependencies": {
      "@babel/core": "^7.14.3",
      ...
      "copy-webpack-plugin": "^12.0.2",
      ...
    }
    ```
3. En `config/webpack.prod.js`, añadir la configuración necesaria para copiar el README y la historia:
    ```js
    const CopyPlugin = require("copy-webpack-plugin");
    const package = require("../package.json");
    const PackageType = package.type;
    const PackageName = package.name.replace("@matter/", "");

    plugins: [
      ...,
      new CopyPlugin({
        patterns: [
          { from: "README.md", to: 'story/' + PackageType + '/' + PackageName },
          { from: "./demo/matter-extradata.stories.js", to: 'story/' + PackageType + '/' + PackageName },
        ],
      }),
    ];
    ```
4. En la carpeta `demo/`, incluir el fichero `matter-extradata.stories.js` que monte la historia en el Storybook.

---

## Producción

### **Publicación del web-component en NEXUS PRO**
👉 [https://nexus.paas.junta-andalucia.es/](https://nexus.paas.junta-andalucia.es/)

1. Eliminar `.npmrc`:
    ```bash
    rm C:\Users\{{USER}}\.npmrc
    ```
2. Actualizar la versión en `package.json`.  
3. Instalar dependencias:
    ```bash
    npm i
    ```
4. Incluir en `package.json` las siguientes líneas:
    ```json
    "files": [
      "dist"
    ]
    ```
5. Generar el compilado:
    ```bash
    npm run build
    ```
6. Configurar el registro:
    ```bash
    npm config set registry https://nexus.paas.junta-andalucia.es/repository/msd.npm-private/
    npm config set @matter:registry=https://nexus.paas.junta-andalucia.es/repository/msd.npm-private/
    ```
7. Autenticarse con el usuario correspondiente:
    ```bash
    npm adduser --registry=https://nexus.paas.junta-andalucia.es/repository/msd.npm-private/ --always-auth
    ```
8. Publicar la nueva versión:
    ```bash
    npm publish
    ```
